### match
```cpp
...
// found in the LICENSE file.
 #include "components/enterprise/client_certificates/core/key_upload_client.h"
 
 >>> 
#include <memory>

 ... 
```
### patch
```cpp
#include "crypto/signature_verifier.h"

```

### match
```cpp
...
 
 namespace client_certificates { ... 
 
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
```cpp
  case crypto::SignatureVerifier::ECDSA_SHA384:

```

