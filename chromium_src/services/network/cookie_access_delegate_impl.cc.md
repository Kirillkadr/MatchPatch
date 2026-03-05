### match
```
...
#include <optional>

 #include <set>
 
 >>> 
#include "base/containers/flat_map.h"

 ... 
```
### patch
```
#include "services/network/cookie_access_delegate_impl.h"
#include <optional>

```

### match
```
...
 namespace network { ... 
 std::optional<FirstPartySetsAccessDelegate::EntriesResult>
CookieAccessDelegateImpl::FindFirstPartySetEntries(
    const base::flat_set<net::SchemefulSite>& sites,
    base::OnceCallback<void(FirstPartySetsAccessDelegate::EntriesResult)>
        callback) const { ... 
return first_party_sets_access_delegate_->FindEntries(sites,
                                                        std::move(callback));
 } 
 >>> 
 ... } ...  
```
### patch
```
bool CookieAccessDelegateImpl::NotUsed() const {
  return false;
}
bool CookieAccessDelegateImpl::ShouldUseEphemeralStorage(
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    base::optional_ref<const url::Origin> top_frame_origin) const {
  if (!cookie_settings_) {
    return false;
  }
  return cookie_settings_->ShouldUseEphemeralStorage(url, site_for_cookies,
                                                     top_frame_origin);
}

```

