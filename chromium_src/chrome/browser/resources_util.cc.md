### match
```cpp
...
#include "ui/chromeos/resources/grit/ui_chromeos_resources_map.h"

 #endif 
 >>> 
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)

#include "brave/grit/brave_theme_resources_map.h"

#define BRAVE_RESOURCES_UTIL                          \
  for (const auto& resource : kBraveThemeResources) { \
    storage.emplace_back(resource.path, resource.id); \
  }

#else
#define BRAVE_RESOURCES_UTIL
#endif  // !BUILDFLAG(IS_ANDROID)


```

### match
```cpp
...
 
 int ResourcesUtil::GetThemeResourceId(const std::string& resource_name) { ... 
return GetThemeIdsMap().GetId(resource_name);
 } 
 >>> 
 ... 
```
### patch
```cpp

#undef BRAVE_RESOURCES_UTIL

```

