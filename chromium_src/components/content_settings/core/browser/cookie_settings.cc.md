### match
```cpp
...
#include <algorithm>

 #include <memory>
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```cpp
#include <optional>
#include "base/check.h"
#include "net/base/features.h"
#include "net/base/url_util.h"

```

### match
```cpp
...
 
 namespace content_settings { ...   >>> 
 void 
 CookieSettings::ShutdownOnUIThread() 
 {  <<< 
DCHECK(thread_checker_.CalledOnValidThread());
 ... } ...  } ...  
```
### patch
```cpp
void CookieSettings::ShutdownOnUIThread_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace content_settings { ... 
 
 ContentSettingsForOneType CookieSettings::GetTpcdMetadataGrants() const { ... 
return tpcd_metadata_manager_ ? tpcd_metadata_manager_->GetGrants()
                                : ContentSettingsForOneType();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void CookieSettings::ShutdownOnUIThread() {
  ShutdownOnUIThread_ChromiumImpl();
  {
    base::AutoLock auto_lock(lock_);
    ephemeral_storage_origins_.clear();
  }
}
bool CookieSettings::ShouldUseEphemeralStorage(
    const url::Origin& origin,
    const net::SiteForCookies& site_for_cookies,
    base::optional_ref<const url::Origin> top_frame_origin,
    url::Origin& storage_origin) {
  const bool should_use = CookieSettingsBase::ShouldUseEphemeralStorage(
      origin.GetURL(), site_for_cookies, top_frame_origin);
  if (!should_use) {
    return false;
  }
  DCHECK(top_frame_origin);
  const std::string ephemeral_storage_domain =
      net::URLToEphemeralStorageDomain(top_frame_origin->GetURL());

  base::AutoLock auto_lock(lock_);
  auto ephemeral_storage_origins_it =
      ephemeral_storage_origins_.find(ephemeral_storage_domain);
  if (ephemeral_storage_origins_it != ephemeral_storage_origins_.end()) {
    const auto& storage_origins = ephemeral_storage_origins_it->second;
    auto storage_origin_it = storage_origins.find(origin);
    if (storage_origin_it != storage_origins.end()) {
      storage_origin = storage_origin_it->second;
      return true;
    }
  } else {
    ephemeral_storage_origins_it =
        ephemeral_storage_origins_
            .emplace(ephemeral_storage_domain,
                     EphemeralStorageOrigins::mapped_type())
            .first;
  }

  url::Origin opaque_origin = origin.DeriveNewOpaqueOrigin();
  ephemeral_storage_origins_it->second[origin] = opaque_origin;
  storage_origin = std::move(opaque_origin);
  return true;
}

std::vector<url::Origin> CookieSettings::TakeEphemeralStorageOpaqueOrigins(
    const std::string& ephemeral_storage_domain) {
  std::vector<url::Origin> result;
  base::AutoLock auto_lock(lock_);
  auto ephemeral_storage_origins_it =
      ephemeral_storage_origins_.find(ephemeral_storage_domain);
  if (ephemeral_storage_origins_it != ephemeral_storage_origins_.end()) {
    result.reserve(ephemeral_storage_origins_it->second.size());
    for (auto& origins : ephemeral_storage_origins_it->second) {
      result.push_back(std::move(origins.second));
    }
    ephemeral_storage_origins_.erase(ephemeral_storage_origins_it);
  }
  return result;
}

```

