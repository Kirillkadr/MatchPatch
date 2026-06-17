### match
```cpp
...
 namespace 
 syncer 
 { 
 >>> 
// Interface for tracking synced DeviceInfo. Note that this includes sync-ing
 ... } ...  
```
### patch
```cpp
class BraveDeviceInfo;

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 class DeviceInfoTracker { ... 
// local device info provider is not initialized, will force update after
 // initialization. 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  virtual void DeleteDeviceInfo(const std::string& client_id, base::OnceClosure callback) { 
  }
  virtual std::vector<std::unique_ptr<BraveDeviceInfo>>
  GetAllBraveDeviceInfo() const;

```

