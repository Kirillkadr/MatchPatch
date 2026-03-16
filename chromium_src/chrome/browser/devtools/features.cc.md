### match
```
...
// found in the LICENSE file.
 #include "chrome/browser/devtools/features.h"
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```
#include "base/feature_override.h"

```

### match
```
...
 
 namespace features { ... 
BASE_FEATURE(kDevToolsGeminiRebranding, base::FEATURE_DISABLED_BY_DEFAULT);
 BASE_FEATURE(kDevToolsAiOriginTrialsApis, base::FEATURE_ENABLED_BY_DEFAULT); 
 >>> 
 ... } ...  
```
### patch
```
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kDevToolsAiCodeCompletion, base::FEATURE_DISABLED_BY_DEFAULT},
#if !BUILDFLAG(IS_ANDROID)
    {kDevToolsConsoleInsights, base::FEATURE_DISABLED_BY_DEFAULT},
#endif  // !BUILDFLAG(IS_ANDROID)
    {kDevToolsNewPermissionDialog, base::FEATURE_DISABLED_BY_DEFAULT},
}});


```

