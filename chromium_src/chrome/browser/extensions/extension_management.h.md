### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
 
 class ExtensionManagement : public KeyedService,
                            public ExtensionManagementClient { ... 
using SettingsUpdateUrlMap =
      base::flat_map<std::string,
                     std::unique_ptr<internal::IndividualSettings>>;
 friend class ExtensionManagementServiceTest; 
 >>> 
// Load all extension management preferences from `pref_service`, and
 ... } ...  } ...  
```
### patch
```
  friend class BraveExtensionManagement;

```

