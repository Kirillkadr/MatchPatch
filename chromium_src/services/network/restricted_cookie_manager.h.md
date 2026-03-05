### match
```
...
 # ifndef ... 
#include <string>

 #include <tuple>
 
 >>> 
#include "base/component_export.h"

 ... 
```
### patch
```
#include "net/base/isolation_info.h"
#include "net/cookies/cookie_access_delegate.h"
#include "net/cookies/cookie_options.h"
#include "net/cookies/site_for_cookies.h"
#include "services/network/public/mojom/restricted_cookie_manager.mojom.h"

```

### match
```
...
 # ifndef ... 
 namespace network { ... 
void SetCanonicalCookieResult(
      const GURL& url,
      const url::Origin& isolated_top_frame_origin,
      const net::CookieSettingOverrides& cookie_setting_overrides,
      const net::SiteForCookies& site_for_cookies,
      const net::CanonicalCookie& cookie,
      bool is_ad_tagged,
      SetCanonicalCookieCallback user_callback,
      net::CookieAccessResult access_result);
 // Called when the Mojo pipe associated with a listener is closed. 
 >>> 
void RemoveChangeListener(Listener* listener);
 ... } ...  
```
### patch
```
  net::CookieOptions MakeOptionsForSet(
      mojom::RestrictedCookieManagerRole role, const GURL& url,
      const net::SiteForCookies& site_for_cookies,
      const CookieSettings& cookie_settings) const;
  net::CookieOptions MakeOptionsForGet(
      mojom::RestrictedCookieManagerRole role, const GURL& url,
      const net::SiteForCookies& site_for_cookies,
      const CookieSettings& cookie_settings) const;                   

```

