### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <utility>
 
 >>> 
#include "base/observer_list.h"

 ...
```
### patch
```cpp
#include <optional>
#include <vector>
#include "base/containers/flat_map.h"
#include "components/content_settings/core/browser/content_settings_provider.h"
#include "components/content_settings/core/browser/host_content_settings_map.h"
#include "components/keyed_service/core/refcounted_keyed_service.h"
#include "net/cookies/site_for_cookies.h"
#include "url/origin.h"

```

### match
```cpp
...
 
 >>> 
void ShutdownOnUIThread() override;
...
```
### patch
```cpp
  void ShutdownOnUIThread_ChromiumImpl();
  bool ShouldUseEphemeralStorage(
      const url::Origin& origin, const net::SiteForCookies& site_for_cookies,
      base::optional_ref<const url::Origin> top_frame_origin,
      url::Origin& storage_origin);
  std::vector<url::Origin> TakeEphemeralStorageOpaqueOrigins(
      const std::string& ephemeral_storage_domain);

 private:
  /* Ephemeral storage domain to non_opaque->opaque origins map. */
  using EphemeralStorageOrigins =
      base::flat_map<std::string, base::flat_map<url::Origin, url::Origin>>;
  EphemeralStorageOrigins ephemeral_storage_origins_ GUARDED_BY(lock_);

 public:

```

