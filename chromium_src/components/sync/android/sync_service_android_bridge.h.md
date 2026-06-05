### match
```cpp
...
 
 namespace syncer { ... 
// the internal value of base::Time.
 int64_t GetLastSyncedTimeForDebugging(); 
 >>> 
void KeepAccountSettingsPrefsOnlyForUsers(
      const std::vector<std::string>& gaia_id_strings);
 ... } ...  
```
### patch
```cpp
  void KeepAccountSettingsPrefsOnlyForUsers_Unused(
      JNIEnv* env, const base::android::JavaRef<jobjectArray>& gaia_ids);

```

