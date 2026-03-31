### match
```cpp
...
#include "crypto/hkdf.h"

 #include "crypto/random.h"
 
 >>> 
namespace {

// Contains base64 random key encrypted with DPAPI.
constexpr char kOsCryptEncryptedKeyPrefName[] = "os_crypt.encrypted_key";

// Whether or not an attempt has been made to enable audit for the DPAPI
// encryption backing the random key.
constexpr char kOsCryptAuditEnabledPrefName[] = "os_crypt.audit_enabled";

// AEAD key length in bytes.
constexpr size_t kKeyLength = 256 / 8;

// AEAD nonce length in bytes.
constexpr size_t kNonceLength = 96 / 8;

// Version prefix for data encrypted with profile bound key.
constexpr char kEncryptionVersionPrefix[] = "v10";

// Key prefix for a key encrypted with DPAPI.
constexpr char kDPAPIKeyPrefix[] = "DPAPI";

bool EncryptStringWithDPAPI(const std::string& plaintext,
                            std::string* ciphertext) {
  DATA_BLOB input;
  input.pbData =
      const_cast<BYTE*>(reinterpret_cast<const BYTE*>(plaintext.data()));
  input.cbData = static_cast<DWORD>(plaintext.length());

  BOOL result = FALSE;
  DATA_BLOB output;
  {
    SCOPED_UMA_HISTOGRAM_TIMER("OSCrypt.Win.Encrypt.Time");
    result = ::CryptProtectData(
        /*pDataIn=*/&input,
        /*szDataDescr=*/
        base::SysUTF8ToWide(
            base::StrCat(
                {version_info::GetProductName(),
                 version_info::IsOfficialBuild() ? "" : " (Developer Build)"}))
            .c_str(),
        /*pOptionalEntropy=*/nullptr,
        /*pvReserved=*/nullptr,
        /*pPromptStruct=*/nullptr, /*dwFlags=*/CRYPTPROTECT_AUDIT,
        /*pDataOut=*/&output);
  }
  base::UmaHistogramBoolean("OSCrypt.Win.Encrypt.Result", result);
  if (!result) {
    PLOG(ERROR) << "Failed to encrypt";
    return false;
  }

  // this does a copy
  ciphertext->assign(reinterpret_cast<std::string::value_type*>(output.pbData),
                     output.cbData);

  LocalFree(output.pbData);
  return true;
}

bool DecryptStringWithDPAPI(const std::string& ciphertext,
                            std::string* plaintext) {
  DATA_BLOB input;
  input.pbData =
      const_cast<BYTE*>(reinterpret_cast<const BYTE*>(ciphertext.data()));
  input.cbData = static_cast<DWORD>(ciphertext.length());

  BOOL result = FALSE;
  DATA_BLOB output;
  {
    SCOPED_UMA_HISTOGRAM_TIMER("OSCrypt.Win.Decrypt.Time");
    result = CryptUnprotectData(&input, nullptr, nullptr, nullptr, nullptr, 0,
                                &output);
  }
  base::UmaHistogramBoolean("OSCrypt.Win.Decrypt.Result", result);
  if (!result) {
    PLOG(ERROR) << "Failed to decrypt";
    return false;
  }

  plaintext->assign(reinterpret_cast<char*>(output.pbData), output.cbData);
  LocalFree(output.pbData);
  return true;
}

// Takes `key` and encrypts it with DPAPI, then stores it in the `local_state`.
// Returns true if the key was successfully encrypted and stored.
bool EncryptAndStoreKey(const std::string& key, PrefService* local_state) {
  std::string encrypted_key;
  if (!EncryptStringWithDPAPI(key, &encrypted_key)) {
    return false;
  }

  // Add header indicating this key is encrypted with DPAPI.
  encrypted_key.insert(0, kDPAPIKeyPrefix);
  std::string base64_key = base::Base64Encode(encrypted_key);
  local_state->SetString(kOsCryptEncryptedKeyPrefName, base64_key);
  return true;
}

}
 ... 
```
### patch
```cpp
#include "base/command_line.h"
#include "brave/components/constants/brave_switches.h"
namespace {
bool IsEncryptionDisabled(const std::string& input_text,
                          std::string* output_text) {
  if (base::CommandLine::ForCurrentProcess()->HasSwitch(
          switches::kDisableEncryptionWin)) {
    *output_text = input_text;
    return true;
  }
  return false;
}

}  // namespace

```

