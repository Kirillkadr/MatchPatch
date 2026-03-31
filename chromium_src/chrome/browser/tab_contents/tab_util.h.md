### match
```cpp
...
 
 # ifndef ... 
 #define CHROME_BROWSER_TAB_CONTENTS_TAB_UTIL_H_
 
 >>> 
#include "content/public/browser/site_instance.h"

 ... 
```
### patch
```cpp
#include "brave/components/containers/buildflags/buildflags.h"

```

### match
```cpp
...
 
 # ifndef ... 
#include "brave/components/containers/buildflags/buildflags.h"

 #include "content/public/browser/site_instance.h"
 
 >>> 
#include "url/gurl.h"

 ... 
```
### patch
```cpp
#include "content/public/browser/storage_partition_config.h"

```

### match
```cpp
...
 
 # ifndef ... 
#include "content/public/browser/storage_partition_config.h"

 #include "url/gurl.h"
 
 >>> 
class Profile
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_CONTAINERS)
#define GetSiteInstanceForNewTab(...) \
  GetSiteInstanceForNewTab(           \
      __VA_ARGS__,                    \
      std::optional<content::StoragePartitionConfig> storage_partition_config)
#endif  // BUILDFLAG(ENABLE_CONTAINERS)


```

### match
```cpp
...
// namespace tab_util
 #endif 
 // CHROME_BROWSER_TAB_CONTENTS_TAB_UTIL_H_ 
 >>> 
 ... 
```
### patch
```cpp

#if BUILDFLAG(ENABLE_CONTAINERS)
#undef GetSiteInstanceForNewTab
#endif  // BUILDFLAG(ENABLE_CONTAINERS)

#endif  // BRAVE_CHROMIUM_SRC_CHROME_BROWSER_TAB_CONTENTS_TAB_UTIL_H_
```

