### match
```
...
// found in the LICENSE file.
 #include "net/url_request/redirect_util.h"
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```
#include <algorithm>
#include <optional>
#include "net/url_request/url_request_job.h"

```

### match
```
...
 namespace net { ...   >>> 
 void 
 RedirectUtil::UpdateHttpRequest 
 (  <<< ... 
const GURL& original_url
 ... ) ...  } ...  
```
### patch
```
void RedirectUtil::UpdateHttpRequest_ChromiumImpl(

```

### match
```
...
 namespace net { ... 
 scoped_refptr<HttpResponseHeaders> RedirectUtil::SynthesizeRedirectHeaders(
    const GURL& redirect_destination,
    ResponseCode response_code,
    const std::string& redirect_reason,
    const HttpRequestHeaders& request_headers) { ... 
return fake_headers;
 } 
 >>> 
 ... } ...  
```
### patch
```
void RedirectUtil::UpdateHttpRequest(
    const GURL& original_url,
    std::string_view original_method,
    const RedirectInfo& redirect_info,
    const std::optional<std::vector<std::string>>& removed_headers,
    const std::optional<net::HttpRequestHeaders>& modified_headers,
    HttpRequestHeaders* request_headers,
    bool* should_clear_upload) {
  UpdateHttpRequest_ChromiumImpl(original_url,
                                 original_method,
                                 redirect_info,
                                 removed_headers,
                                 modified_headers,
                                 request_headers,
                                 should_clear_upload);
  // Hack for capping referrers at the network layer.
  if (removed_headers) {
    if (std::ranges::contains(*removed_headers, "X-Brave-Cap-Referrer")) {
      GURL capped_referrer = URLRequestJob::ComputeReferrerForPolicy(
          ReferrerPolicy::REDUCE_GRANULARITY_ON_TRANSITION_CROSS_ORIGIN,
          GURL(redirect_info.new_referrer), redirect_info.new_url);
      const_cast<RedirectInfo&>(redirect_info).new_referrer =
          capped_referrer.spec();
    }
  }
}

```

