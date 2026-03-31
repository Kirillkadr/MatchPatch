### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <vector>
 
 >>> 
#include "base/lazy_instance.h"

 ... 
```
### patch
```cpp
#include "base/lazy_instance.h"
#include "components/content_settings/core/browser/content_settings_info.h"
#include "components/content_settings/core/browser/content_settings_utils.h"
#include "components/content_settings/core/browser/website_settings_info.h"
#include "components/content_settings/core/common/content_settings.h"
#include "components/content_settings/core/common/content_settings_types.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
~ContentSettingsRegistry();
 void Init(); 
 >>> 
// Register a new content setting. This maps an origin to an ALLOW/ASK/BLOCK
 ... } ...  
```
### patch
```cpp
  void RegisterBraveContentSettingsTypes(const ContentSettingsType& type,
                                         const std::string& name);
  void BraveInit();

```

