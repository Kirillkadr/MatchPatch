### match
```cpp
...
 
 namespace syncer { ... 
 
 class SyncUserSettings { ... 
// Clears per account prefs for all users *except* the ones in the passed-in
 // `available_gaia_ids`. 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  virtual void KeepAccountSettingsPrefsOnlyForUsers_Unused(
      const std::vector<GaiaId>& available_gaia_ids) {} 

```

