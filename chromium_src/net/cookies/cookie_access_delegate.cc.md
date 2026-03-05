### match
```
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "net/cookies/cookie_access_delegate.h"

 ... 
```
### patch
```
#include "net/cookies/cookie_access_delegate.h"

```

### match
```
...
#include "net/cookies/cookie_access_delegate.h"

 #include "net/cookies/cookie_access_delegate.h"
 
 >>> 
class GURL
 ... 
```
### patch
```
#include <optional>

#include "base/notreached.h"

```

### match
```
...
 namespace net { ... 
 bool CookieAccessDelegate::ShouldTreatUrlAsTrustworthy(const GURL& url) const { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```
bool CookieAccessDelegate::NotUsed() const {
  return false;
}
bool CookieAccessDelegate::ShouldUseEphemeralStorage(
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    base::optional_ref<const url::Origin> top_frame_origin) const {
  NOTREACHED() << "Should be overridden";
}

```

