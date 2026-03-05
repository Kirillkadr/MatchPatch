### match
```
...
 # ifndef ... 
#include <stddef.h>

 #include <stdint.h>
 
 >>> 
#include <map>

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
#include "net/log/net_log_with_source.h"

 #include "url/gurl.h"
 >>> 
 ...
```
### patch
```
#define CookieMonster ChromiumCookieMonster

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 class NET_EXPORT CookieMonster::PersistentCookieStore
    : public RefcountedPersistentCookieStore { ... 
private:
  friend class base::RefCountedThreadSafe<PersistentCookieStore>;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
#undef CookieMonster
class NET_EXPORT CookieMonster : public ChromiumCookieMonster {
 public:
  // These constructors and destructors must be kept in sync with those in
  // Chromium's CookieMonster.
  CookieMonster(scoped_refptr<PersistentCookieStore> store,
                NetLog* net_log,
                std::unique_ptr<PrefDelegate> pref_delegate = nullptr);
  CookieMonster(scoped_refptr<PersistentCookieStore> store,
                base::TimeDelta last_access_threshold,
                NetLog* net_log,
                std::unique_ptr<PrefDelegate> pref_delegate);
  ~CookieMonster() override;
  // CookieStore implementation.
  //
  // This only includes methods that needs special behavior to deal with
  // our collection of ephemeral monsters.
  void DeleteCanonicalCookieAsync(const CanonicalCookie& cookie,
                                  DeleteCallback callback) override;
  void DeleteAllCreatedInTimeRangeAsync(
      const CookieDeletionInfo::TimeRange& creation_range,
      DeleteCallback callback) override;
  void DeleteAllMatchingInfoAsync(CookieDeletionInfo delete_info,
                                  DeleteCallback callback) override;
  void DeleteSessionCookiesAsync(DeleteCallback) override;
  void SetCookieableSchemes(std::vector<std::string> schemes,
                            SetCookieableSchemesCallback callback) override;

  void SetCanonicalCookieAsync(
      std::unique_ptr<CanonicalCookie> cookie,
      const GURL& source_url,
      const CookieOptions& options,
      SetCookiesCallback callback,
      std::optional<CookieAccessResult> cookie_access_result =
          std::nullopt) override;
  void GetCookieListWithOptionsAsync(
      const GURL& url,
      const CookieOptions& options,
      const CookiePartitionKeyCollection& cookie_partition_key_collection,
      GetCookieListCallback callback) override;

 private:
  NetLogWithSource net_log_;
  std::map<std::string, std::unique_ptr<ChromiumCookieMonster>>
      ephemeral_cookie_stores_;
  ChromiumCookieMonster* GetOrCreateEphemeralCookieStoreForTopFrameURL(
      const GURL& top_frame_url);
};

```

