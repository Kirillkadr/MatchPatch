### match
```cpp
...
// found in the LICENSE file.
 #include "components/feed/feed_feature_list.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp
#include "base/feature_override.h"
#include "build/build_config.h"

```

### match
```cpp
...
 
 namespace feed { ... 
 
 bool IsWebFeedEnabledForLocale(const std::string& country) { ... 
return std::ranges::contains(launched_countries, country) &&
         !base::FeatureList::IsEnabled(kWebFeedKillSwitch);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
#if BUILDFLAG(IS_ANDROID)
    {kFeedContainment, base::FEATURE_DISABLED_BY_DEFAULT},
    {kInterestFeedV2, base::FEATURE_DISABLED_BY_DEFAULT},
#endif
}});

```

