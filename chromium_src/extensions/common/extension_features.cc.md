### match
```cpp
...
// found in the LICENSE file.
 #include "extensions/common/extension_features.h"
 
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
 
 namespace extensions_features { ... 
 
 BASE_FEATURE ( ... 
kWebRequestPersistFilteredEventsViaEventRouter,
             
 base::FEATURE_ENABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kExtensionManifestV2Disabled, base::FEATURE_DISABLED_BY_DEFAULT},
    {kExtensionManifestV2Unsupported, base::FEATURE_DISABLED_BY_DEFAULT},
    {kExtensionsManifestV3Only, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

