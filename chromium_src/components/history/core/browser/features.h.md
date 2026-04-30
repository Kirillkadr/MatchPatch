### match
```cpp
...
 
 # ifndef ... 
#include <limits.h>

 #include <string>
 
 >>> 
#include "base/component_export.h"

 ... 
```
### patch
```cpp
#include "base/feature_list.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace history { ... 
COMPONENT_EXPORT(HISTORY_FEATURES)
 BASE_DECLARE_FEATURE(kHistoryDatabaseWriteAheadLogging); 
 >>> 
 ... } ...  
```
### patch
```cpp
COMPONENT_EXPORT(HISTORY_FEATURES)
BASE_DECLARE_FEATURE(kHistoryMoreSearchResults);

```

