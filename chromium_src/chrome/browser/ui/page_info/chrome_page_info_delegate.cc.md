### match
```cpp
...
#include "chrome/browser/ui/page_info/chrome_page_info_delegate.h"

 #include "base/metrics/histogram_functions.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/content_settings/core/browser/brave_content_settings_utils.h"

```

### match
```cpp
...
 
 void ChromePageInfoDelegate::SetSecurityStateForTests(
    security_state::SecurityLevel security_level,
    security_state::VisibleSecurityState visible_security_state) { ... 
visible_security_state_for_tests_ = visible_security_state;
 } 
 >>> 
 ... 
```
### patch
```cpp
bool ChromePageInfoDelegate::BraveShouldShowPermission(
    ContentSettingsType type) {
  if ((content_settings::IsShieldsContentSettingsType(type) ||
       type == ContentSettingsType::GEOLOCATION) &&
      GetProfile()->IsTor()) {
    return false;
  }
  return true;
}


```

