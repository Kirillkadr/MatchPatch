### match
```cpp
...
// found in the LICENSE file.
 #include "components/webapps/browser/features.h"
 
 >>> 
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
 namespace 
 features 
 { 
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kWebAppsEnableMLModelForPromotion, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

