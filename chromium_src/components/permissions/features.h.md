### match
```cpp
...
 
 # ifndef ... 
 namespace 
 features 
 { 
 >>> 
#if BUILDFLAG(IS_ANDROID)
COMPONENT_EXPORT(PERMISSIONS_COMMON)
BASE_DECLARE_FEATURE(kAndroidWindowManagementWebApi);

COMPONENT_EXPORT(PERMISSIONS_COMMON)
BASE_DECLARE_FEATURE(kAndroidItemChooserCancelButton);
#endif
 ... } ...  
```
### patch
```cpp
COMPONENT_EXPORT(PERMISSIONS_COMMON)
BASE_DECLARE_FEATURE(kPermissionLifetime);

```

