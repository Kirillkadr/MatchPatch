### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
// Reset the instance for use inside tests.
 void ResetForTesting(); 
 >>> 
const PermissionSettingsInfo* Get(ContentSettingsType type) const;
 ... } ...  
```
### patch
```cpp
  void Unregister(ContentSettingsType type) {
    permission_settings_info_.erase(type);
  }
  void ResetForTesting_Unused();

```

