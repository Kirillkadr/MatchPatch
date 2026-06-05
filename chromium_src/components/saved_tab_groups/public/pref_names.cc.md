### match
```cpp
...
// found in the LICENSE file.
 #include "components/saved_tab_groups/public/pref_names.h"
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include "components/pref_registry/pref_registry_syncable.h"

```

### match
```cpp
...
 
 namespace tab_groups::prefs { ... 
>>> 
 void 
 RegisterProfilePrefs(user_prefs::PrefRegistrySyncable* registry) 
 { 
<<< 
// Disables cross-device syncing for older clients. For newer clients,
 ... } ...  } ...  
```
### patch
```cpp
void RegisterProfilePrefs_ChromiumImpl(user_prefs::PrefRegistrySyncable* registry) {

```

### match
```cpp
...
 
 namespace tab_groups::prefs { ... 
 
 void KeepAccountSettingsPrefsOnlyForUsers(
    PrefService* pref_service,
    const std::vector<signin::GaiaIdHash>& available_gaia_ids) { ... 
syncer::KeepAccountKeyedPrefValuesOnlyForUsers(
      pref_service, prefs::kLocallyClosedRemoteTabGroupIds, available_gaia_ids);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void RegisterProfilePrefs(user_prefs::PrefRegistrySyncable* registry) {
  RegisterProfilePrefs_ChromiumImpl(registry);
#if BUILDFLAG(IS_ANDROID)
  registry->SetDefaultPrefValue(prefs::kAutoOpenSyncedTabGroups,
                                base::Value(false));
#endif  // BUILDFLAG(IS_ANDROID)
}

```

