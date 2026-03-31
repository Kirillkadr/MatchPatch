### match
```cpp
...
#include <vector>

 #include "base/feature_list.h"
 
 >>> 
#include "base/functional/bind.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 void DisplayMediaAccessHandler::WebContentsDestroyed(
    WebContents* web_contents) { ... 
pending_requests_.erase(web_contents);
 } 
 >>> 
 ... 
```
### patch
```cpp
// Upstream enabled this feature via finch field trial. We need this feature
// enabled as well as it addresses a security exploit.
OVERRIDE_FEATURE_DEFAULT_STATES({{
#if !BUILDFLAG(IS_ANDROID)
    // Upstream field trial only enabled this feature on desktop platforms.
    {kDisplayMediaRejectLongDomains, base::FEATURE_ENABLED_BY_DEFAULT},
#endif
}});
```

