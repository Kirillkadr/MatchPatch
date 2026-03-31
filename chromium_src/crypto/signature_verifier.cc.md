### match
```cpp
...
#include "crypto/signature_verifier.h"

 #include <memory>
 
 >>> 
#include "base/check_op.h"

 ...
```
### patch
```cpp
#include "brave/chromium_src/crypto/signature_verifier.h"  // IWYU pragma: export

```

### match
```cpp
... 
    case RSA_PKCS1_SHA1:
      pkey_type = EVP_PKEY_RSA;
      digest = EVP_sha1();
      break;
    case RSA_PKCS1_SHA256:
    case RSA_PSS_SHA256:
      pkey_type = EVP_PKEY_RSA;
      digest = EVP_sha256();
      
 break; 
 >>> 
 ...
```
### patch
```cpp
    case ECDSA_SHA384:
  pkey_type = EVP_PKEY_EC;
  digest = EVP_sha384();
  break;

```

