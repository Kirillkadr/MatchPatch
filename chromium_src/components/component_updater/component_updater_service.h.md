### match
```cpp
...
 
 namespace update_client { ... 
 } 
 // namespace update_client 
 >>> 
namespace extensions {
class AutotestPrivateLoadSmartDimComponentFunction;
}
 ... 
```
### patch
```cpp
namespace chrome {
namespace android {
class BraveComponentUpdaterAndroid;
}
}  // namespace chrome
namespace brave_component_updater {
class BraveOnDemandUpdater;
}

```

### match
```cpp
...
 
 namespace component_updater { ... 
 
 class ComponentUpdateService { ... 
friend class speech::SodaInstallerImpl;
 friend class ::ComponentsHandler; 
 >>> 
FRIEND_TEST_ALL_PREFIXES(ComponentInstallerTest, RegisterComponent);
 ... } ...  } ...  
```
### patch
```cpp
  friend class ::chrome::android::BraveComponentUpdaterAndroid;

```

### match
```cpp
...
 
 namespace component_updater { ... 
 
 class OnDemandUpdater { ... 
enum class Priority { BACKGROUND = 0, FOREGROUND = 1 };
 virtual ~OnDemandUpdater() = default; 
 >>> 
private
 ... } ...  } ...  
```
### patch
```cpp
  private:                                                                 \
  friend class brave_component_updater::BraveOnDemandUpdater;             \
                                                                          \
  virtual void EnsureInstalled(const std::string& id, Callback callback); \
  virtual void OnDemandUpdate(const std::vector<std::string>& ids,        \
                              Priority priority, Callback callback);      \
                                                                          \
 public:

```

