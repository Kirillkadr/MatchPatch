### match
```
...
#include <iterator>

 #include <memory>
 
 >>> 
#include "base/containers/fixed_flat_map.h"

 ... 
```
### patch
```
#include "services/network/cookie_settings.h"
#include <optional>

#include "net/base/features.h"
#include "url/origin.h"

```

### match
```
...
 namespace network { ... 
 bool CookieSettings::ShouldAlwaysAllowCookiesForTesting(
    const GURL& url,
    const GURL& first_party_url) const { ... 
return ShouldAlwaysAllowCookies(url, first_party_url);
 } 
 >>> 
 ... } ...  
```
### patch
```
bool CookieSettings::IsEphemeralCookieAccessible(
    const net::CanonicalCookie& cookie,
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    const std::optional<url::Origin>& top_frame_origin,
    const net::FirstPartySetMetadata& first_party_set_metadata,
    net::CookieSettingOverrides overrides,
    net::CookieInclusionStatus* cookie_inclusion_status) const {
  // Upstream now do single cookie-specific checks in some places to determine
  // whether cookie access should be granted. However, when ephemeral storage is
  // enabled, Brave doesn't care about whether access is being requested for a
  // specific cookie or not, so we simply return |true| if that's the case.
  // See https://crrev.com/c/2895004 for the upstream change that required this.
  if (IsEphemeralCookieAccessAllowed(url, site_for_cookies, top_frame_origin,
                                     overrides,
                                     /*cookie_partition_key=*/std::nullopt)) {
    return true;
  }

  return IsCookieAccessible(cookie, url, site_for_cookies, top_frame_origin,
                            first_party_set_metadata, overrides,
                            cookie_inclusion_status);
}

net::NetworkDelegate::PrivacySetting
CookieSettings::IsEphemeralPrivacyModeEnabled(
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    const std::optional<url::Origin>& top_frame_origin,
    net::CookieSettingOverrides overrides) const {
  if (IsEphemeralCookieAccessAllowed(url, site_for_cookies, top_frame_origin,
                                     overrides,
                                     /*cookie_partition_key=*/std::nullopt)) {
    return net::NetworkDelegate::PrivacySetting::kStateAllowed;
  }

  return IsPrivacyModeEnabled(url, site_for_cookies, top_frame_origin,
                              overrides);
}

bool CookieSettings::AnnotateAndMoveUserBlockedEphemeralCookies(
    const GURL& url,
    const net::SiteForCookies& site_for_cookies,
    const url::Origin* top_frame_origin,
    const net::FirstPartySetMetadata& first_party_set_metadata,
    net::CookieSettingOverrides overrides,
    net::CookieAccessResultList& maybe_included_cookies,
    net::CookieAccessResultList& excluded_cookies) const {
  std::optional<url::Origin> top_frame_origin_opt;
  if (top_frame_origin)
    top_frame_origin_opt = *top_frame_origin;

  if (IsEphemeralCookieAccessAllowed(url, site_for_cookies,
                                     top_frame_origin_opt, overrides,
                                     /*cookie_partition_key=*/std::nullopt)) {
    return true;
  }

  return AnnotateAndMoveUserBlockedCookies(
      url, site_for_cookies, top_frame_origin, first_party_set_metadata,
      overrides, maybe_included_cookies, excluded_cookies);
}

```

