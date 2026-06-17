### match
```cpp
...
 #include "url/gurl.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/components/sync_device_info/brave_device_info.h"
#include "components/history/core/browser/history_service.h"
#include "components/sync_device_info/device_info_tracker.h"
#include "testing/gmock/include/gmock/gmock.h"
#include "testing/gtest/include/gtest/gtest.h"

```

### match
```cpp
...
 using testing::_; 
 >>> 
 ... 
```
### patch
```cpp
namespace syncer {
class BraveDeviceInfoTracker : public syncer::BraveDeviceInfoTracker {
 public:
  MOCK_CONST_METHOD0(GetAllBraveDeviceInfo,
                     std::vector<std::unique_ptr<BraveDeviceInfo>>());
};

}  // namespace syncer

```

