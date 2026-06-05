### match
```cpp
...
#include <string>

 #include <vector>
 
 >>> 
#include "base/feature_list.h"

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
 >>> 
// If enabled, shows a confirm dialog before removing search suggestions from
// the New Tab page real search box ("realbox").
BASE_FEATURE(kConfirmSuggestionRemovals,
             "ConfirmNtpSuggestionRemovals",
             base::FEATURE_DISABLED_BY_DEFAULT);
...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kCustomizeChromeSidePanelExtensionsCard,
     base::FEATURE_DISABLED_BY_DEFAULT},
    {kCustomizeChromeWallpaperSearch, base::FEATURE_DISABLED_BY_DEFAULT},
    {kNtpAlphaBackgroundCollections, base::FEATURE_DISABLED_BY_DEFAULT},
    {kNtpBackgroundImageErrorDetection, base::FEATURE_DISABLED_BY_DEFAULT},
    {kNtpChromeCartModule, base::FEATURE_DISABLED_BY_DEFAULT},
    {kNtpModulesMaxColumnCount, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

