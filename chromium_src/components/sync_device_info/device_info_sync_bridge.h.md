### match
```cpp
...
 #include <vector>
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/components/sync_device_info/brave_device_info.h"
#include "components/sync_device_info/device_info_tracker.h"

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 class DeviceInfoSyncBridge : public DataTypeSyncBridge,
                             public DeviceInfoTracker { ... 
// compared with the local copy. If the data has been updated, then it will be
 // committed. Otherwise nothing happens. 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void RefreshLocalDeviceInfoIfNeeded_ChromiumImpl();

```

### match
```cpp
...
 
 namespace syncer { ... 
// For testing only.
 bool IsPulseTimerRunningForTest() const; 
 >>> 
 ... } ...  
```
### patch
```cpp
  void DeleteDeviceInfo(const std::string& client_id, base::OnceClosure callback)
      override;
  std::vector<std::unique_ptr<BraveDeviceInfo>> GetAllBraveDeviceInfo()
      const override;

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 class DeviceInfoSyncBridge : public DataTypeSyncBridge,
                             public DeviceInfoTracker { ... 
 // Store SyncData in the cache and durable storage. 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void OnDeviceInfoDeleted(const std::string& client_id, const int attempt, 
                      base::OnceClosure callback);

```

