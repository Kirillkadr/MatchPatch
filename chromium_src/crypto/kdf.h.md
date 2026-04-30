### match
```cpp
...
 
 # ifndef ... 
 #define CRYPTO_KDF_H_
 
 >>> 
#include "base/containers/span.h"

 ... 
```
### patch
```cpp
#include "base/check_op.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace crypto::kdf { ... 
 
 std::array<uint8_t, N> Hkdf(crypto::hash::HashKind kind,
                            base::span<const uint8_t> secret,
                            base::span<const uint8_t> salt,
                            base::span<const uint8_t> info) { ... 
return out;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// Upstream function DeriveKeyScrypt has a CHECK_EQ(rv, 1) which we don't
// want as we shouldn't crash the browser because of bad input data, so this
// is our own version of the same function but returning a bool instead of
// CHECKing.
CRYPTO_EXPORT bool DeriveKeyScryptNoCheck(const ScryptParams& params,
                                          base::span<const uint8_t> password,
                                          base::span<const uint8_t> salt,
                                          base::span<uint8_t> result);

struct Pbkdf2HmacSha256Params {
  // BoringSSL uses a uint32_t for the iteration count for PBKDF2, so we match
  // that.
  uint32_t iterations = 0;
};

CRYPTO_EXPORT bool DeriveKeyPbkdf2HmacSha256(
    const kdf::Pbkdf2HmacSha256Params& params,
    base::span<const uint8_t> password,
    base::span<const uint8_t> salt,
    base::span<uint8_t> result);

struct Pbkdf2HmacSha512Params {
  // BoringSSL uses a uint32_t for the iteration count for PBKDF2, so we match
  // that.
  uint32_t iterations = 0;
};

CRYPTO_EXPORT bool DeriveKeyPbkdf2HmacSha512(
    const kdf::Pbkdf2HmacSha512Params& params,
    base::span<const uint8_t> password,
    base::span<const uint8_t> salt,
    base::span<uint8_t> result);

```

