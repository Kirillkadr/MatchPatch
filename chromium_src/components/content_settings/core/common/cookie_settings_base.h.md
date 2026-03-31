### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <variant>
 
 >>> 
#include "base/containers/fixed_flat_set.h"

 ... 
```
### patch
```cpp
#include <optional>

#include "components/content_settings/core/common/content_settings.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
 
 class CookieSettingsBase { ... 
//
 // This may be called on any thread. 
 >>> 
bool IsCookieSessionOnly(const GURL& url) const;
 ... } ...  } ...  
```
### patch
```cpp
  bool ShouldUseEphemeralStorage(                                                  
      const GURL& url, const net::SiteForCookies& site_for_cookies,
      base::optional_ref<const url::Origin> top_frame_origin) const;
  bool IsEphemeralCookieAccessAllowed(
      const GURL& url, const net::SiteForCookies& site_for_cookies,
      base::optional_ref<const url::Origin> top_frame_origin,
      net::CookieSettingOverrides overrides,
      base::optional_ref<const net::CookiePartitionKey> cookie_partition_key,
      CookieSettingWithMetadata* cookie_settings = nullptr) const;
  bool IsFullCookieAccessAllowed_ChromiumImpl(
      const GURL& url, const net::SiteForCookies& site_for_cookies,
      base::optional_ref<const url::Origin> top_frame_origin,
      net::CookieSettingOverrides overrides,
      base::optional_ref<const net::CookiePartitionKey> cookie_partition_key,
      CookieSettingWithMetadata* cookie_settings = nullptr) const;
  bool ShouldBlockThirdPartyIfSettingIsExplicit(
      bool block_third_party_cookies, ContentSetting cookie_setting,
      bool is_explicit_setting, bool is_first_party_allowed_scheme) const;

 public:

```

