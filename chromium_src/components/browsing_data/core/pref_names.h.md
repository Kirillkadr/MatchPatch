### match
```cpp
...
 
 # ifndef ... 
 
 namespace browsing_data::prefs { ... 
void MaybeMigrateToQuickDeletePrefValues(PrefService* pref_service);
 #endif 
 // BUILDFLAG(IS_IOS) 
 >>> 
 ... } ...  
```
### patch
```cpp
inline constexpr char kDeleteBrowsingHistoryOnExit[] =
    "browser.clear_data.browsing_history_on_exit";
inline constexpr char kDeleteDownloadHistoryOnExit[] =
    "browser.clear_data.download_history_on_exit";
inline constexpr char kDeleteCacheOnExit[] = "browser.clear_data.cache_on_exit";
inline constexpr char kDeleteCookiesOnExit[] =
    "browser.clear_data.cookies_on_exit";
inline constexpr char kDeletePasswordsOnExit[] =
    "browser.clear_data.passwords_on_exit";
inline constexpr char kDeleteFormDataOnExit[] =
    "browser.clear_data.form_data_on_exit";
inline constexpr char kDeleteHostedAppsDataOnExit[] =
    "browser.clear_data.hosted_apps_data_on_exit";
inline constexpr char kDeleteSiteSettingsOnExit[] =
    "browser.clear_data.site_settings_on_exit";
inline constexpr char kDeleteBraveLeoHistory[] = "browser.clear_data.brave_leo";
inline constexpr char kDeleteBraveLeoHistoryOnExit[] =
    "browser.clear_data.brave_leo_on_exit";

```

