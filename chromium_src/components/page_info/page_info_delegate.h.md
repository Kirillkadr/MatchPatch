### match
```cpp
...
 
 # ifndef ... 
 
 class PageInfoDelegate { ... 
std::unique_ptr<
      content_settings::PageSpecificContentSettings::Delegate>
 GetPageSpecificContentSettingsDelegate() 
 = 
 0 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  virtual bool BraveShouldShowPermission(ContentSettingsType type) = 0; 

```

