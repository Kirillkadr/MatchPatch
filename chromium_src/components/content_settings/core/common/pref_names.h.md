### match
```cpp
...
 
 namespace prefs { ... 
inline constexpr char kDesktopSiteWindowSettingEnabled[] =
    "desktop_site.window_setting";
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
/ Preferences that are exclusively used to store managed values for default
// content settings.
inline constexpr char kManagedDefaultBraveAdblockSetting[] =
    "brave.profile.managed_default_content_settings.brave_adblock";
inline constexpr char kManagedDefaultBraveHttpsUpgrade[] =
    "brave.profile.managed_default_content_settings.brave_https_upgrade";
inline constexpr char kManagedDefaultBraveReferrersSetting[] =
    "brave.profile.managed_default_content_settings.brave_referrers";
inline constexpr char kManagedDefaultBraveRemember1PStorageSetting[] =
    "brave.profile.managed_default_content_settings.brave_remember_1p_storage";

```

