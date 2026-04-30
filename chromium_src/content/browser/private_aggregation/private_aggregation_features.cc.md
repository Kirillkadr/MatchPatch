### match
```cpp
...
// found in the LICENSE file.
 #include "content/browser/private_aggregation/private_aggregation_features.h"
 
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
 
 namespace content { ... 
 
 BASE_FEATURE ( ... 
 base::FEATURE_ENABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kPrivateAggregationApiDebugModeRequires3pcEligibility,
     base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

