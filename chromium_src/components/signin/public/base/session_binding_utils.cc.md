### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/signin/public/base/session_binding_utils.h"

 ... 
```
### patch
```cpp
#include "components/signin/public/base/session_binding_utils.h"

```

### match
```cpp
...
 
 namespace signin { ... 
 
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
  return "SHA384";     

```

