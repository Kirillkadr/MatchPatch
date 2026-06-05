### match
```cpp
...
#define COMPONENTS_SUPERVISED_USER_CORE_BROWSER_SUPERVISED_USER_CONTENT_SETTINGS_PROVIDER_H_

 // A content setting provider that is set by the custodian of a supervised user. 
 >>> 
#include "base/callback_list.h"

 ... 
```
### patch
```cpp
#include "build/build_config.h"
#if !BUILDFLAG(IS_IOS)
#include "brave/components/content_settings/core/browser/brave_global_value_map.h"
#endif

```

### match
```cpp
...
 
 namespace supervised_user { ... 
void OnSupervisedSettingsAvailable(const base::DictValue& settings);
 content_settings::GlobalValueMap value_map_; 
 >>> 
// Used around accesses to the |value_map_| object to guarantee
 ... } ...  
```
### patch
```cpp
#if !BUILDFLAG(IS_IOS)
  content_settings::BraveGlobalValueMap value_map_;
#endif

```

