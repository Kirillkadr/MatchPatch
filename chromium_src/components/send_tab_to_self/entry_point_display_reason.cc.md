### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/send_tab_to_self/entry_point_display_reason.h"

 ... 
```
### patch
```cpp
#include "components/send_tab_to_self/entry_point_display_reason.h"

```

### match
```cpp
...
>>>
 std::optional<EntryPointDisplayReason> 
 GetEntryPointDisplayReason 
 ( 
<<< 
const GURL& url_to_share
 ... ) ...  
```
### patch
```cpp
std::optional<EntryPointDisplayReason> GetEntryPointDisplayReason_ChromiumImpl(

```

### match
```cpp
...
 
 namespace send_tab_to_self { ... 
 
 namespace internal { ... 
 
 std::optional<EntryPointDisplayReason> GetEntryPointDisplayReason_ChromiumImpl(
const GURL& url_to_share,
    syncer::SyncService* sync_service,
    SendTabToSelfModel* send_tab_to_self_model,
    PrefService* pref_service) { ... 
return EntryPointDisplayReason::kOfferFeature;
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
std::optional<EntryPointDisplayReason> GetEntryPointDisplayReason(
    const GURL& url_to_share,
    syncer::SyncService* sync_service,
    SendTabToSelfModel* send_tab_to_self_model,
    PrefService* pref_service) {
  std::optional<send_tab_to_self::EntryPointDisplayReason> reason =
      GetEntryPointDisplayReason_ChromiumImpl(
          url_to_share, sync_service, send_tab_to_self_model, pref_service);
  if (!reason) {
    return reason;
  }
  // We do not want to show any UI suggesting that the user signs into their
  // account. There used to be an upstream flag that disabled this
  // functionality, but it was removed. Even without the flag, we are not
  // hitting either of these right now, but if the upstream code changes we'd
  // still want to prevent the UI from showing.
  if (*reason == EntryPointDisplayReason::kInformNoTargetDevice ||
      *reason == EntryPointDisplayReason::kOfferSignIn) {
    return std::nullopt;
  }
  return reason;
}

```

