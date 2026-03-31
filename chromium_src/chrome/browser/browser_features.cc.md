### match
```cpp
...
#include "chrome/browser/browser_features.h"

 #include "base/feature_list.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ...
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
BASE_FEATURE(kRemovalOfIWAsFromTabCapture, base::FEATURE_ENABLED_BY_DEFAULT);

 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kBookmarkTriggerForPrerender2KillSwitch, base::FEATURE_ENABLED_BY_DEFAULT},
    {kCertificateTransparencyAskBeforeEnabling,
     base::FEATURE_ENABLED_BY_DEFAULT},

    {kBookmarkTriggerForPrefetch, base::FEATURE_DISABLED_BY_DEFAULT},
    {kDestroyProfileOnBrowserClose, base::FEATURE_DISABLED_BY_DEFAULT},
    // Google has asked embedders not to enforce these pins:
    // https://groups.google.com/a/chromium.org/g/embedder-dev/c/XsNTwEiN1lI/m/TMXh-ZvOAAAJ
    {kNewTabPageTriggerForPrerender2, base::FEATURE_DISABLED_BY_DEFAULT},
#if !BUILDFLAG(IS_ANDROID)
    {kReportPakFileIntegrity, base::FEATURE_DISABLED_BY_DEFAULT},
#endif  // BUILDFLAG(IS_ANDROID)

}});

```

