### match
```cpp
...
// found in the LICENSE file.
 #include "content/browser/file_system_access/features.h"
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 namespace content::features { ... 
// 1/2GiB
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kFileSystemAccessDirectoryIterationBlocklistCheck,
     base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

