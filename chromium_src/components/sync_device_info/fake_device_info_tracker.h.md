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
 
 class FakeDeviceInfoTracker : public DeviceInfoTracker { ... 
CountActiveDevicesByType()
      
 const 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void DeleteDeviceInfo(const std::string& client_id, base::OnceClosure callback) 
      override;
  std::vector<std::unique_ptr<BraveDeviceInfo>> GetAllBraveDeviceInfo()
      const override;

```

