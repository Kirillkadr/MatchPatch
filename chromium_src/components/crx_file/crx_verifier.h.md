### match
```cpp
...
 
 # ifndef ... 
 #define COMPONENTS_CRX_FILE_CRX_VERIFIER_H_
 
 >>> 
#include <stdint.h>

 ... 
```
### patch
```cpp
#include "base/containers/span.h"

```

### match
```cpp
...
 
 # ifndef ... 
 namespace 
 crx_file 
 { 
 >>> 
enum class VerifierFormat {
  CRX3,                            // Accept only Crx3.
  CRX3_WITH_TEST_PUBLISHER_PROOF,  // Accept only Crx3 with a test or production
                                   // publisher proof.
  CRX3_WITH_PUBLISHER_PROOF,       // Accept only Crx3 with a production
                                   // publisher proof.
}
 ... } ...  
```
### patch
```cpp
void SetBravePublisherKeyHashForTesting(base::span<const uint8_t> test_key);

```

