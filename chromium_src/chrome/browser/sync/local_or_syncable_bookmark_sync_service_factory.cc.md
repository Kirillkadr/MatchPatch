### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/sync/local_or_syncable_bookmark_sync_service_factory.h"
 
 >>> 
#include "chrome/browser/profiles/profile.h"

 ... 
```
### patch
```cpp
#include "build/build_config.h"
#include "chrome/browser/profiles/profile_keyed_service_factory.h"

```

### match
```cpp
...
#include "components/sync/model/wipe_model_upon_sync_disabled_behavior.h"

 #include "components/sync_bookmarks/bookmark_sync_service.h"
 
 >>> 
// static
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)
#include "brave/browser/ui/bookmark/bookmark_prefs_service_factory.h"

// Adding BookmarkPrefsServiceFactory as dependency because kShowBookmarBar and
// kAlwaysShowBookmarkBarOnNTP manage bookmark bar state together and need to
// register both prefs at same time.
#define ProfileKeyedServiceFactory(...)                    \
  ProfileKeyedServiceFactory(__VA_ARGS__) {                \
    DependsOn(BookmarkPrefsServiceFactory::GetInstance()); \
  }                                                        \
  void LocalOrSyncableBookmarkSyncServiceFactory_Unused()
#endif


```

### match
```cpp
...
 
 std::unique_ptr<KeyedService> LocalOrSyncableBookmarkSyncServiceFactory::
    BuildServiceInstanceForBrowserContext(
        content::BrowserContext* context) const { ... 
return std::make_unique<sync_bookmarks::BookmarkSyncService>(
      syncer::WipeModelUponSyncDisabledBehavior::kNever);
 } 
 >>> 
 ... 
```
### patch
```cpp

#if !BUILDFLAG(IS_ANDROID)
#undef ProfileKeyedServiceFactory
#endif
```

