### match
```cpp
...
#include <algorithm>

 #include <utility>
 
 >>> 
#include "base/feature.h"

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
 
 namespace safe_browsing { ... 
 
 base::ListValue GetFeatureStatusList() { ... 
return param_list;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kClientSideDetectionClipboardCopyApi, base::FEATURE_DISABLED_BY_DEFAULT},
    {kGooglePlayProtectInApkTelemetry, base::FEATURE_DISABLED_BY_DEFAULT},
    {kNotificationTelemetry, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

