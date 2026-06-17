### match
```cpp
...
// found in the LICENSE file.
 #include "components/sync_device_info/fake_device_info_tracker.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/components/sync_device_info/brave_device_info.h"

```

### match
```cpp
...
 namespace 
 syncer 
 { 
 >>> 
 ... } ...  
```
### patch
```cpp
void FakeDeviceInfoTracker::DeleteDeviceInfo(const std::string& client_id,
                                             base::OnceClosure callback) {}
std::vector<std::unique_ptr<BraveDeviceInfo>>
FakeDeviceInfoTracker::GetAllBraveDeviceInfo() const {
  return std::vector<std::unique_ptr<BraveDeviceInfo>>();
}

```

