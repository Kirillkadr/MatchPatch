### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
 
 namespace features { ... 
COMPONENT_EXPORT(CONTENT_SETTINGS_FEATURES)
 extern const char kUseTestMetadataName[]; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
COMPONENT_EXPORT(CONTENT_SETTINGS_FEATURES)
BASE_DECLARE_FEATURE(kAllowIncognitoPermissionInheritance);

```

