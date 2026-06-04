### match
```cpp
...
 
 # ifndef ... 
 
 namespace password_manager { ... 
 public 
 : 
 >>> 
static void RegisterProfilePrefs(user_prefs::PrefRegistrySyncable* registry);
 ... } ...  
```
### patch
```cpp
  static void RegisterProfilePrefs_ChromiumImpl(               
      user_prefs::PrefRegistrySyncable* registry);

```

