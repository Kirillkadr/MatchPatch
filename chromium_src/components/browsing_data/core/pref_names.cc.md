### match
```cpp
...
// found in the LICENSE file.
 #include "components/browsing_data/core/pref_names.h"
 
 >>> 
#include "base/metrics/histogram_macros.h"

 ... 
```
### patch
```cpp
#include "brave/chromium_src/components/browsing_data/core/pref_names.h"

```

### match
```cpp
...
 
 namespace browsing_data::prefs { ...   >>> 
 void 
 RegisterBrowserUserPrefs(user_prefs::PrefRegistrySyncable* registry) 
 {  <<< 
registry->RegisterListPref(kBrowsingDataLifetime);
 ... } ...  } ...  
```
### patch
```cpp
void RegisterBrowserUserPrefs_ChromiumImpl(user_prefs::PrefRegistrySyncable* registry) {

```

### match
```cpp
...
 
 namespace browsing_data::prefs { ... 
void MaybeMigrateToQuickDeletePrefValues(PrefService* pref_service) {
  bool migratedToQuickDeletePrefValues =
      pref_service->GetBoolean(kMigratedToQuickDeletePrefValues);

  if (migratedToQuickDeletePrefValues) {
    return;
  }

  bool migrateToNewDefaults = AreAllSelectionPrefsDefaultValue(pref_service);

  if (migrateToNewDefaults) {
    pref_service->SetInteger(
        kDeleteTimePeriod,
        static_cast<int>(browsing_data::TimePeriod::LAST_15_MINUTES));
    pref_service->SetBoolean(kCloseTabs, true);
  } else {
    pref_service->SetBoolean(kCloseTabs, false);
  }

  UMA_HISTOGRAM_BOOLEAN("Privacy.DeleteBrowsingData.MigratedToNewDefaults",
                        migrateToNewDefaults);

  pref_service->SetBoolean(kMigratedToQuickDeletePrefValues, true);
}
 #endif 
 // BUILDFLAG(IS_IOS) 
 >>> 
 ... } ...  
```
### patch
```cpp
void RegisterBrowserUserPrefs(user_prefs::PrefRegistrySyncable* registry) {
  RegisterBrowserUserPrefs_ChromiumImpl(registry);
  registry->RegisterBooleanPref(kDeleteBrowsingHistoryOnExit, false);
  registry->RegisterBooleanPref(kDeleteDownloadHistoryOnExit, false);
  registry->RegisterBooleanPref(kDeleteCacheOnExit, false);
  registry->RegisterBooleanPref(kDeleteCookiesOnExit, false);
  registry->RegisterBooleanPref(kDeletePasswordsOnExit, false);
  registry->RegisterBooleanPref(kDeleteFormDataOnExit, false);
  registry->RegisterBooleanPref(kDeleteHostedAppsDataOnExit, false);
  registry->RegisterBooleanPref(kDeleteSiteSettingsOnExit, false);
  registry->RegisterBooleanPref(kDeleteBraveLeoHistory, false);
  registry->RegisterBooleanPref(kDeleteBraveLeoHistoryOnExit, false);
}

```

