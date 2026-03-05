### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class SharedWorkerContentSettingsProxy : public WebContentSettingsClient { ... 
~SharedWorkerContentSettingsProxy() override;
 // WebContentSettingsClient overrides. 
 >>> 
bool AllowStorageAccessSync(StorageType storage_type) override;
 ... } ...  } ...  
```
### patch
```
  bool UnusedFunction() {                                                
    return false;
  }
  brave_shields::mojom::ShieldsSettingsPtr GetBraveShieldsSettings(
      ContentSettingsType webcompat_settings_type) override;

```

