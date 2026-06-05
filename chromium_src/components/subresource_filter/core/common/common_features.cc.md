### match
```cpp
...
// found in the LICENSE file.
 #include "components/subresource_filter/core/common/common_features.h"
 
 >>> 
namespace subresource_filter {

BASE_FEATURE(kAdTagging, base::FEATURE_ENABLED_BY_DEFAULT);
BASE_FEATURE(kSubresourceFilterPrewarm, base::FEATURE_DISABLED_BY_DEFAULT);

}
 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 namespace subresource_filter { ... 
BASE_FEATURE(kAdTagging, base::FEATURE_ENABLED_BY_DEFAULT);
 BASE_FEATURE(kSubresourceFilterPrewarm, base::FEATURE_DISABLED_BY_DEFAULT); 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kAdTagging, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

