### match
```
...
#include "chrome/browser/enterprise/connectors/device_trust/key_management/core/network/key_upload_request.h"

 #include "base/check.h"
 
 >>> 
#include "chrome/browser/enterprise/connectors/device_trust/key_management/core/signing_key_pair.h"

 ... 
```
### patch
```
#include "brave/chromium_src/crypto/signature_verifier.h"  // IWYU pragma: export

```

### match
```
...
 
 namespace enterprise_connectors { ... 
 
 namespace { ... 
 
 BPKUR::KeyType AlgorithmToType(
    crypto::SignatureVerifier::SignatureAlgorithm algorithm) { ... 
 case 
 crypto::SignatureVerifier::ECDSA_SHA256 
 : 
 >>> 
return BPKUR::EC_KEY;
 ... } ...  } ...  } ...  
```
### patch
```
    case crypto::SignatureVerifier::ECDSA_SHA384:

```

