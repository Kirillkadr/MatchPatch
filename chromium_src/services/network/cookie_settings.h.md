### match
```
...
 # ifndef ... 
#include <string>

 #include <vector>
 
 >>> 
#include "base/component_export.h"

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
 namespace network { ... 
// the cookie is secure and returns true if the cookie should be deleted on
 // exit. 
 >>> 
DeleteCookiePredicate CreateDeleteCookieOnExitPredicate() const;
 ... } ...  
```
### patch
```
  bool IsEphemeralCookieAccessible(
      const net::CanonicalCookie& cookie, const GURL& url,
      const net::SiteForCookies& site_for_cookies,
      const std::optional<url::Origin>& top_frame_origin,
      const net::FirstPartySetMetadata& first_party_set_metadata,
      net::CookieSettingOverrides overrides,
      net::CookieInclusionStatus* cookie_inclusion_status) const;
  net::NetworkDelegate::PrivacySetting IsEphemeralPrivacyModeEnabled(
      const GURL& url, const net::SiteForCookies& site_for_cookies,
      const std::optional<url::Origin>& top_frame_origin,
      net::CookieSettingOverrides overrides) const;
  bool AnnotateAndMoveUserBlockedEphemeralCookies(
      const GURL& url, const net::SiteForCookies& site_for_cookies,
      const url::Origin* top_frame_origin,
      const net::FirstPartySetMetadata& first_party_set_metadata,
      net::CookieSettingOverrides overrides,
      net::CookieAccessResultList& maybe_included_cookies,
      net::CookieAccessResultList& excluded_cookies) const;

```

