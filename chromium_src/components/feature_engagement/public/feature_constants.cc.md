### match
```cpp
...
// found in the LICENSE file.
 #include "components/feature_engagement/public/feature_constants.h"
 
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
 
 namespace feature_engagement { ... 
BASE_FEATURE(kIPHResumptionRailFeature,
             "IPH_ResumptionRail",
             base::FEATURE_ENABLED_BY_DEFAULT);
 #endif 
 // !BUILDFLAG(IS_IOS) 
 >>> 
 ... } ...  
```
### patch
```cpp
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC) || BUILDFLAG(IS_LINUX)
BASE_FEATURE(kIPHBraveShieldsInPageInfoFeature,
             "IPH_BraveShieldsInPageInfo",
             base::FEATURE_ENABLED_BY_DEFAULT);
#endif
OVERRIDE_FEATURE_DEFAULT_STATES({{
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_APPLE) || BUILDFLAG(IS_LINUX)
    {kIPHGMCCastStartStopFeature, base::FEATURE_DISABLED_BY_DEFAULT},
    {kIPHPasswordsManagementBubbleAfterSaveFeature,
     base::FEATURE_DISABLED_BY_DEFAULT},
    {kIPHPdfInkSignaturesFeature, base::FEATURE_DISABLED_BY_DEFAULT},
    {kIPHTabGroupsSaveV2IntroFeature, base::FEATURE_DISABLED_BY_DEFAULT},
    {kIPHTabSearchToolbarButtonFeature, base::FEATURE_DISABLED_BY_DEFAULT},
#endif
}});

```

