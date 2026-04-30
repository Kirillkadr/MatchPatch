### match
```cpp
...
// found in the LICENSE file.
 #include "components/omnibox/common/omnibox_features.h"
 
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
 
 namespace omnibox { ... 
 
 namespace flag_descriptions { ... 
const char kOmniboxDebugLogsDescription[] =
    "Enables logging that can be read from an internals page.";
 } 
 // namespace flag_descriptions 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kAblateSearchProviderWarmup, base::FEATURE_ENABLED_BY_DEFAULT},
    {kDocumentProviderNoSyncRequirement, base::FEATURE_DISABLED_BY_DEFAULT},
    {kMlUrlScoring, base::FEATURE_DISABLED_BY_DEFAULT},
#if BUILDFLAG(IS_ANDROID)
    {kOmniboxMobileParityUpdateV2, base::FEATURE_DISABLED_BY_DEFAULT},
#endif
    {kRichAutocompletion, base::FEATURE_DISABLED_BY_DEFAULT},
    {kStarterPackExpansion, base::FEATURE_DISABLED_BY_DEFAULT},
}});

BASE_FEATURE(kOmniboxTabSwitchByDefault,
             base::FEATURE_DISABLED_BY_DEFAULT);


```

