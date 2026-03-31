### match
```cpp
...
#include "base/feature_list.h"

 #include "base/values.h"
 
 >>> 
#include "chrome/browser/profiles/profile.h"

 ... 
```
### patch
```cpp
#include "brave/components/brave_shields/core/browser/brave_shields_utils.h"
#include "chrome/browser/content_settings/host_content_settings_map_factory.h"

```

### match
```cpp
...
#include "components/security_interstitials/core/https_only_mode_metrics.h"

 #include "content/public/browser/web_contents.h"
 
 >>> 
#include "net/base/url_util.h"

 ... 
```
### patch
```cpp
#include "content/public/browser/navigation_handle.h"

```

### match
```cpp
...
#include "net/base/url_util.h"

 #include "url/gurl.h"
 
 >>> 
using HttpInterstitialState =
    security_interstitials::https_only_mode::HttpInterstitialState;
 ... 
```
### patch
```cpp
namespace {

bool NormalWindowHttpsOnly(const GURL& url, Profile* profile) {
  if (profile->IsIncognitoProfile()) {
    return false;
  }
  HostContentSettingsMap* map =
      HostContentSettingsMapFactory::GetForProfile(profile);
  return brave_shields::ShouldForceHttps(map, url);
}

}  // namespace


```

