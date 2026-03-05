### match
```
...
 # ifndef ... 
 #define SERVICES_NETWORK_COOKIE_ACCESS_DELEGATE_IMPL_H_
 
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
#include "base/component_export.h"

 ... 
```
### patch
```
#include "net/cookies/cookie_access_delegate.h"

```

### match
```
...
 # ifndef ... 
 namespace network { ... 
;
 // net::CookieAccessDelegate implementation: 
 >>> 
bool ShouldTreatUrlAsTrustworthy(const GURL& url) const override;
 ... } ...  
```
### patch
```
  bool NotUsed() const override;
  bool ShouldUseEphemeralStorage(
      const GURL& url, const net::SiteForCookies& site_for_cookies,
      base::optional_ref<const url::Origin> top_frame_origin) const override; 

```

