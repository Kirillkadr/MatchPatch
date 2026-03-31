### match
```cpp

...
#include "net/url_request/url_request_job.h"

 #include <utility>
 
 >>> 
#include "base/compiler_specific.h"

 ... 
```
### patch
```cpp

#include "base/strings/string_util.h"

```

### match
```cpp

...
 
 namespace net { ... 
 
 namespace { ... 
GURL MaybeStripToOrigin(GURL url, bool should_strip_to_origin) {
  if (!should_strip_to_origin)
    return url;

  return url.DeprecatedGetOriginAsURL();
}
 } 
 // namespace 
 >>> 
// static
 ... } ...  
```
### patch
```cpp

// Strip referrer for cross-origin requests from a .onion hostname.
// This also affects the Origin header outside of CORS requests.

```

### match
```cpp

...
 
 namespace net { ... 
 GURL 
 URLRequestJob::ComputeReferrerForPolicy 
 ( 
 >>> 
ReferrerPolicy policy
 ... ) ...  } ...  
```
### patch
```cpp

      ReferrerPolicy policy, const GURL& original_referrer,
      const GURL& destination, bool* same_origin_out_for_metrics) {
    if (base::EndsWith(original_referrer.host(), ".onion",
                       base::CompareCase::INSENSITIVE_ASCII) &&
        !url::IsSameOriginWith(original_referrer, destination)) {
      return GURL();
    }
    return ComputeReferrerForPolicy_Chromium(
        policy, original_referrer, destination, same_origin_out_for_metrics);
  }
  GURL URLRequestJob::ComputeReferrerForPolicy_Chromium(

```

