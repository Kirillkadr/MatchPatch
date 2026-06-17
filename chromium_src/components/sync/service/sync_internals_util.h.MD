### match
```cpp
...
 
 namespace syncer { ... 
 
 namespace sync_ui_util { ... 
// If `include_sensitive_data` is false, Personally Identifiable Information
 // won't be included in the return value. 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
base::DictValue ConstructAboutInformation_ChromiumImpl(
    IncludeSensitiveData include_sensitive_data,
    SyncService* service,
    const std::string& channel);

```

