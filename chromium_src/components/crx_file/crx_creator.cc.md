### match
```cpp
...
// found in the LICENSE file.
 #include "components/crx_file/crx_creator.h"
 
 >>> 
#include "base/files/file.h"

 ... 
```
### patch
```cpp
#include "base/check.h"

```

### match
```cpp
...
 namespace 
 crx_file 
 { 
 >>> 
namespace {

std::string GetCrxId(base::span<const uint8_t> key) {
  const auto full_hash = crypto::hash::Sha256(key);
  const auto truncated_hash = base::span(full_hash).first<16>();
  return std::string(base::as_string_view(truncated_hash));
}

constexpr size_t kFileBufferSize = 1 << 12;

// Read to the end of the file, updating the signer.
CreatorResult ReadAndSignArchive(base::File* file,
                                 crypto::sign::Signer& signer,
                                 std::vector<uint8_t>* signature) {
  std::array<uint8_t, kFileBufferSize> buffer;
  std::optional<size_t> read;
  while ((read = file->ReadAtCurrentPos(buffer)).value_or(0) > 0) {
    signer.Update(base::span(buffer).first(*read));
  }
  if (!read.has_value()) {
    return CreatorResult::ERROR_SIGNING_FAILURE;
  }
  *signature = signer.Finish();
  return CreatorResult::OK;
}

bool WriteArchive(base::File* out, base::File* in) {
  std::array<uint8_t, kFileBufferSize> buffer;
  std::optional<size_t> read;
  in->Seek(base::File::Whence::FROM_BEGIN, 0);
  while ((read = in->ReadAtCurrentPos(buffer)).value_or(0) > 0) {
    auto to_write = base::span<const uint8_t>(buffer).first(*read);
    if (!out->WriteAtCurrentPosAndCheck(to_write)) {
      return false;
    }
  }
  // A successful final read at the end of the file is indicated by returning a
  // populated option with a read size of 0. An unpopulated option indicates a
  // read error.
  return read.has_value() && read.value() == 0;
}

CreatorResult SignArchiveAndCreateHeader(
    const base::FilePath& output_path,
    base::File* file,
    const crypto::keypair::PrivateKey& signing_key,
    CrxFileHeader* header) {
  // Get the public key.
  std::vector<uint8_t> public_key = signing_key.ToSubjectPublicKeyInfo();

  // Assemble SignedData section.
  SignedData signed_header_data;
  signed_header_data.set_crx_id(GetCrxId(public_key));
  const std::string signed_header_data_str =
      signed_header_data.SerializeAsString();
  const auto signed_header_size_octets =
      base::I32ToLittleEndian(signed_header_data_str.size());

  // Create a signer, init with purpose, SignedData length, run SignedData
  // through, run ZIP through.
  crypto::sign::Signer signer(crypto::sign::SignatureKind::RSA_PKCS1_SHA256,
                              signing_key);
  signer.Update(base::as_byte_span(kSignatureContext));
  signer.Update(signed_header_size_octets);
  signer.Update(base::as_byte_span(signed_header_data_str));

  if (!file->IsValid()) {
    return CreatorResult::ERROR_FILE_NOT_READABLE;
  }
  std::vector<uint8_t> signature;
  const CreatorResult signing_result =
      ReadAndSignArchive(file, signer, &signature);
  if (signing_result != CreatorResult::OK) {
    return signing_result;
  }
  AsymmetricKeyProof* proof = header->add_sha256_with_rsa();
  proof->set_public_key(base::as_string_view(public_key));
  proof->set_signature(base::as_string_view(signature));
  header->set_signed_header_data(signed_header_data_str);
  return CreatorResult::OK;
}

CreatorResult WriteCRX(const CrxFileHeader& header,
                       const base::FilePath& output_path,
                       base::File* file) {
  const std::string header_str = header.SerializeAsString();
  const auto header_size_octets = base::I32ToLittleEndian(header_str.size());

  const auto format_version_octets = std::to_array<uint8_t>({3, 0, 0, 0});
  base::File crx(output_path,
                 base::File::FLAG_CREATE_ALWAYS | base::File::FLAG_WRITE);
  if (!crx.IsValid()) {
    return CreatorResult::ERROR_FILE_NOT_WRITABLE;
  }
  if (!crx.WriteAtCurrentPosAndCheck(kCrxFileHeaderMagic) ||
      !crx.WriteAtCurrentPosAndCheck(format_version_octets) ||
      !crx.WriteAtCurrentPosAndCheck(header_size_octets) ||
      !crx.WriteAtCurrentPosAndCheck(base::as_byte_span(header_str)) ||
      !WriteArchive(&crx, file)) {
    return CreatorResult::ERROR_FILE_WRITE_FAILURE;
  }
  return CreatorResult::OK;
}

}
 ... } ...  
```
### patch
```cpp
class CrxFileHeader;
std::string GetCrxId_BraveImpl(base::span<const uint8_t> key,
                               CrxFileHeader* header);
                               // Override for GetCrxId() in SignArchiveAndCreateHeader() to generate the
// correct signed data for the second signature.
std::string GetCrxId_BraveImpl(base::span<const uint8_t> key,
                               CrxFileHeader* header) {
  if (header->sha256_with_rsa_size() > 0) {
    const AsymmetricKeyProof& first_proof = header->sha256_with_rsa()[0];
    return GetCrxId(base::as_byte_span(first_proof.public_key()));
  }
  return GetCrxId(key);
}

CreatorResult CreateWithMultipleKeys(
    const base::FilePath& output_path,
    const base::FilePath& zip_path,
    base::span<const crypto::keypair::PrivateKey> keys) {
  CrxFileHeader header;
  base::File file(zip_path, base::File::FLAG_OPEN | base::File::FLAG_READ);
  for (const auto& key : keys) {
    file.Seek(base::File::Whence::FROM_BEGIN, 0);
    const CreatorResult signing_result =
        SignArchiveAndCreateHeader(output_path, &file, key, &header);
    if (signing_result != CreatorResult::OK) {
      return signing_result;
    }
  }

  return WriteCRX(header, output_path, &file);

```

