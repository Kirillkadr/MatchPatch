### match
```cpp
...
#define COMPONENTS_SEND_TAB_TO_SELF_ENTRY_POINT_DISPLAY_REASON_H_

 #include <optional>
 
 >>> 
class GURL
 ... 
```
### patch
```cpp
#include <optional>
namespace send_tab_to_self {
namespace internal {

std::optional<EntryPointDisplayReason> GetEntryPointDisplayReason(
    const GURL& url_to_share,
    syncer::SyncService* sync_service,
    SendTabToSelfModel* send_tab_to_self_model,
    PrefService* pref_service);

}  // namespace internal

}  // namespace send_tab_to_self

```

### match
```cpp
...
>>>
std::optional<EntryPointDisplayReason> GetEntryPointDisplayReason(
    const GURL& url_to_share,
    syncer::SyncService* sync_service,
    SendTabToSelfModel* send_tab_to_self_model,
    PrefService* pref_service);
<<< 
 ...  
```
### patch
```cpp
std::optional<EntryPointDisplayReason> GetEntryPointDisplayReason_ChromiumImpl(
    const GURL& url_to_share,
    syncer::SyncService* sync_service,
    SendTabToSelfModel* send_tab_to_self_model,
    PrefService* pref_service);

```

