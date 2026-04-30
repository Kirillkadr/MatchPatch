### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
using const_iterator = MapValueIterator<typename Map::const_iterator,
                                          const WebsiteSettingsInfo*>;
 static WebsiteSettingsRegistry* GetInstance(); 
 >>> 
WebsiteSettingsRegistry(const WebsiteSettingsRegistry&) = delete;
 ... } ...  
```
### patch
```cpp
  void Unregister(ContentSettingsType type) {
    website_settings_info_.erase(type);
  }                                           
  static WebsiteSettingsRegistry* GetInstance_Unused();

```

