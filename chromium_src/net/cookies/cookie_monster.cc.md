### match
```
...
#include <utility>

 #include <vector>
 
 >>> 
#include "base/check.h"

 ...
```
### patch
```
#include <memory>
#include <optional>
#include "net/base/url_util.h"
#include "net/cookies/cookie_monster.h"

```

### match
```
...
// notification of key load completion triggered by the first request for the
 // same eTLD+1. 
 >>> 
static const int kMinutesIn400Days = 60 * 24 * 400;
 ...
```
### patch
```
#define CookieMonster ChromiumCookieMonster

```

### match
```
... 
return std::ranges::any_of(partitioned_cookies_, [&](const auto& pair) {
    const auto& [other_key, cookie_map] = pair;
    return other_key != partition_key &&
           !CookiePartitionKey::HasNonce(other_key) &&
           cookie_map->contains(domain);
 } 
 >>> 
 ...
```
### patch
```
#undef CookieMonster
CookieMonster::CookieMonster(scoped_refptr<PersistentCookieStore> store,
                             NetLog* net_log,
                             std::unique_ptr<PrefDelegate> pref_delegate)
    : ChromiumCookieMonster(store, net_log, std::move(pref_delegate)),
      net_log_(
          NetLogWithSource::Make(net_log, NetLogSourceType::COOKIE_STORE)) {}
CookieMonster::CookieMonster(scoped_refptr<PersistentCookieStore> store,
                             base::TimeDelta last_access_threshold,
                             NetLog* net_log,
                             std::unique_ptr<PrefDelegate> pref_delegate)
    : ChromiumCookieMonster(store,
                            last_access_threshold,
                            net_log,
                            std::move(pref_delegate)),
      net_log_(
          NetLogWithSource::Make(net_log, NetLogSourceType::COOKIE_STORE)) {}

CookieMonster::~CookieMonster() {}

ChromiumCookieMonster*
CookieMonster::GetOrCreateEphemeralCookieStoreForTopFrameURL(
    const GURL& top_frame_url) {
  std::string domain = URLToEphemeralStorageDomain(top_frame_url);
  auto it = ephemeral_cookie_stores_.find(domain);
  if (it != ephemeral_cookie_stores_.end())
    return it->second.get();

  return ephemeral_cookie_stores_
      .emplace(domain, new ChromiumCookieMonster(nullptr /* store */,
                                                 net_log_.net_log()))
      .first->second.get();
}

void CookieMonster::DeleteCanonicalCookieAsync(const CanonicalCookie& cookie,
                                               DeleteCallback callback) {
  for (auto& it : ephemeral_cookie_stores_) {
    it.second->DeleteCanonicalCookieAsync(cookie, DeleteCallback());
  }
  ChromiumCookieMonster::DeleteCanonicalCookieAsync(cookie,
                                                    std::move(callback));
}

void CookieMonster::DeleteAllCreatedInTimeRangeAsync(
    const CookieDeletionInfo::TimeRange& creation_range,
    DeleteCallback callback) {
  for (auto& it : ephemeral_cookie_stores_) {
    it.second->DeleteAllCreatedInTimeRangeAsync(creation_range,
                                                DeleteCallback());
  }
  ChromiumCookieMonster::DeleteAllCreatedInTimeRangeAsync(creation_range,
                                                          std::move(callback));
}

void CookieMonster::DeleteAllMatchingInfoAsync(CookieDeletionInfo delete_info,
                                               DeleteCallback callback) {
  if (delete_info.ephemeral_storage_domain.has_value()) {
    ephemeral_cookie_stores_.erase(*delete_info.ephemeral_storage_domain);
    std::move(callback).Run(0);
    return;
  }

  for (auto& it : ephemeral_cookie_stores_) {
    it.second->DeleteAllMatchingInfoAsync(delete_info, DeleteCallback());
  }
  ChromiumCookieMonster::DeleteAllMatchingInfoAsync(delete_info,
                                                    std::move(callback));
}

void CookieMonster::DeleteSessionCookiesAsync(DeleteCallback callback) {
  for (auto& it : ephemeral_cookie_stores_) {
    it.second->DeleteSessionCookiesAsync(DeleteCallback());
  }
  ChromiumCookieMonster::DeleteSessionCookiesAsync(std::move(callback));
}

void CookieMonster::SetCookieableSchemes(
    std::vector<std::string> schemes,
    SetCookieableSchemesCallback callback) {
  for (auto& it : ephemeral_cookie_stores_) {
    it.second->SetCookieableSchemes(schemes, SetCookieableSchemesCallback());
  }
  ChromiumCookieMonster::SetCookieableSchemes(std::move(schemes),
                                              std::move(callback));
}

void CookieMonster::SetCanonicalCookieAsync(
    std::unique_ptr<CanonicalCookie> cookie,
    const GURL& source_url,
    const CookieOptions& options,
    SetCookiesCallback callback,
    std::optional<CookieAccessResult> cookie_access_result) {
  if (options.should_use_ephemeral_storage()) {
    if (!options.top_frame_origin()) {
      // Shouldn't happen, but don't do anything in this case.
      net::CookieInclusionStatus cookie_inclusion_status;
      cookie_inclusion_status.AddExclusionReason(
          net::CookieInclusionStatus::ExclusionReason::EXCLUDE_UNKNOWN_ERROR);

      MaybeRunCookieCallback(std::move(callback),
                             CookieAccessResult(cookie_inclusion_status));
      return;
    }
    ChromiumCookieMonster* ephemeral_monster =
        GetOrCreateEphemeralCookieStoreForTopFrameURL(
            options.top_frame_origin()->GetURL());
    ephemeral_monster->SetCanonicalCookieAsync(std::move(cookie), source_url,
                                               options, std::move(callback),
                                               std::move(cookie_access_result));
    return;
  }

  ChromiumCookieMonster::SetCanonicalCookieAsync(
      std::move(cookie), source_url, options, std::move(callback),
      std::move(cookie_access_result));
}

void CookieMonster::GetCookieListWithOptionsAsync(
    const GURL& url,
    const CookieOptions& options,
    const CookiePartitionKeyCollection& cookie_partition_key_collection,
    GetCookieListCallback callback) {
  if (options.should_use_ephemeral_storage()) {
    if (!options.top_frame_origin()) {
      // Shouldn't happen, but don't do anything in this case.
      MaybeRunCookieCallback(std::move(callback), CookieAccessResultList(),
                             CookieAccessResultList());
      return;
    }
    ChromiumCookieMonster* ephemeral_monster =
        GetOrCreateEphemeralCookieStoreForTopFrameURL(
            options.top_frame_origin()->GetURL());
    ephemeral_monster->GetCookieListWithOptionsAsync(
        url, options, cookie_partition_key_collection, std::move(callback));
    return;
  }

  ChromiumCookieMonster::GetCookieListWithOptionsAsync(
      url, options, cookie_partition_key_collection, std::move(callback));
}

```