### match
```
...
 
 # ifndef ... 
#include "net/socket/connection_attempts.h"

 #include "net/url_request/url_request_job.h"
 
 >>> 
#if BUILDFLAG(ENABLE_DEVICE_BOUND_SESSIONS)
#include "net/device_bound_sessions/session_service.h"
#endif
 ... 
```
### patch
```
#include "net/base/isolation_info.h"
#include "net/base/request_priority.h"
#include "net/cookies/cookie_options.h"

```

### match
```
...
 
 # ifndef ... 
 
 namespace net { ... 
 
 class NET_EXPORT_PRIVATE URLRequestHttpJob : public URLRequestJob { ... 
void OnStartCompleted(int result);
 void OnReadCompleted(int result); 
 >>> 
void NotifyBeforeStartTransactionCallback(
      int result,
      const std::optional<HttpRequestHeaders>& headers);
 ... } ...  } ...  
```
### patch
```
  CookieOptions CreateCookieOptions(
      CookieOptions::SameSiteCookieContext same_site_context) const;

```

