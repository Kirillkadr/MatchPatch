### match
```cpp
...
 
 # ifndef ... 
 
 namespace component_updater { ... 
 
 class CrxUpdateService : public ComponentUpdateService,
                         public ComponentUpdateService::Observer,
                         public OnDemandUpdater { ... 
void OnEvent(const CrxUpdateItem& item) override;
 // Overrides for OnDemandUpdater. 
 >>> 
void OnDemandUpdate(const std::string& id,
                      Priority priority,
                      Callback callback) override;
 ... } ...  } ...  
```
### patch
```cpp
  void OnDemandUpdate(const std::vector<std::string>& ids, Priority priority,   
                 Callback callback) override;
  void EnsureInstalled(const std::string& id, Callback callback) override;

```

