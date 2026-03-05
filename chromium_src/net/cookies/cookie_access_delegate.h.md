### match
```
...
 # ifndef ... 
 #define NET_COOKIES_COOKIE_ACCESS_DELEGATE_H_
 
 >>> 
#include <optional>

 ... 
```
### patch
```
#include <optional>

```

### match
```
...
 # ifndef ... 
#include <optional>

 #include <optional>
 
 >>> 
#include "base/containers/flat_map.h"

 ... 
```
### patch
```
#include "base/types/optional_ref.h"
#include "net/cookies/cookie_setting_override.h"
#include "net/cookies/site_for_cookies.h"
#include "url/gurl.h"
#include "url/origin.h"

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT CookieAccessDelegate { ... 
// method on a URL that would already be treated as secure by default, e.g. an
 // https:// one has no effect. 
 >>> 
virtual bool ShouldTreatUrlAsTrustworthy(const GURL& url) const;
 ... } ...  } ...  
```
### patch
```
  virtual bool ShouldUseEphemeralStorage(
      const GURL& url, const net::SiteForCookies& site_for_cookies,
      base::optional_ref<const url::Origin> top_frame_origin) const;

```

