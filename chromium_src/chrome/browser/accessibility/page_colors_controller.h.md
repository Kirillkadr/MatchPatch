### match
```
...
 # ifndef ... 
static void RegisterProfilePrefs(PrefRegistrySimple* registry);  >>> 
 static void MigrateObsoleteProfilePrefs(PrefService* profile_prefs);  <<< ... 
// ui::NativeThemeObserver:
 ... 
```
### patch
```
  static void MigrateObsoleteProfilePrefs_ChromiumImpl(PrefService* profile_prefs);

```

