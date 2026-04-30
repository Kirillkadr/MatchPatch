### match
```cpp
...
// found in the LICENSE file.
 #include "components/history_clusters/core/on_device_clustering_features.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 namespace history_clusters { ... 
 
 namespace features { ... 
 
 BASE_FEATURE ( ... 
 base::FEATURE_DISABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kOnDeviceClustering, base::FEATURE_DISABLED_BY_DEFAULT},
    {kOnDeviceClusteringKeywordFiltering, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

