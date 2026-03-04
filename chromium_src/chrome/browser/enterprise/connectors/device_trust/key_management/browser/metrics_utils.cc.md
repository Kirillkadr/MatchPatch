### match
```
...
#include "base/metrics/histogram_functions.h"

 #include "base/strings/stringprintf.h"
 
 >>> 
#include "crypto/signature_verifier.h"

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
 
 DTKeyType AlgorithmToType(
    crypto::SignatureVerifier::SignatureAlgorithm algorithm) { ... 
 case 
 crypto::SignatureVerifier::ECDSA_SHA256 
 : 
 >>> 
return DTKeyType::kEc;
 ... } ...  } ...  } ...  
```
### patch
```
    case crypto::SignatureVerifier::ECDSA_SHA384:

```

