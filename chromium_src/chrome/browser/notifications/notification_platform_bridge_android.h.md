### match
```cpp
...
 
 # ifndef ... 
static void RegisterProfilePrefs(user_prefs::PrefRegistrySyncable* registry);
 private 
 : 
 >>> 
void OnNotificationProcessed(const std::string& notification_id);
 ... 
```
### patch
```cpp
 friend class BraveNotificationPlatformBridgeHelperAndroid;

```

