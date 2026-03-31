### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/sharing_hub/sharing_hub_features.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 namespace sharing_hub { ... 
void RegisterProfilePrefs(PrefRegistrySimple* registry) {
  registry->RegisterBooleanPref(prefs::kDesktopSharingHubEnabled, true);
}
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kDesktopScreenshots, base::FEATURE_ENABLED_BY_DEFAULT},
}});

```

