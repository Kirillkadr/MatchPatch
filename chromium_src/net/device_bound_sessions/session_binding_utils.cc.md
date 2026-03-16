### match
```cpp

...
#include <optional>

 #include <string_view>
 
 >>> 
#include "base/base64url.h"

 ... 
```
### patch
```cpp

#include "net/device_bound_sessions/session_binding_utils.h"

```

### match
```cpp

...
 namespace net::device_bound_sessions { ... 
 namespace { ... 
 std::string SignatureAlgorithmToString(
    crypto::SignatureVerifier::SignatureAlgorithm algorithm) { ... 
 case crypto : ... 
 return "PS256"; 
 >>> 
 ... } ...  } ...  } ...  
```
### patch
```cpp

    case crypto::SignatureVerifier::ECDSA_SHA384:
  return "SHA384";     \

```

