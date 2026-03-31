### match
```cpp
...
 
 # ifndef ... 
 #define COMPONENTS_CRX_FILE_CRX_CREATOR_H_
 
 >>> 
#include <string>

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
enum class CreatorResult {
  OK,  // The CRX file was successfully created.
  ERROR_SIGNING_FAILURE,
  ERROR_FILE_NOT_READABLE,
  ERROR_FILE_NOT_WRITABLE,
  ERROR_FILE_WRITE_FAILURE,
}
 ... } ...  
```
### patch
```cpp
CreatorResult CreateWithMultipleKeys(
    const base::FilePath& output_path,
    const base::FilePath& zip_path,
    base::span<const crypto::keypair::PrivateKey> keys);

```

