### match
```cpp
...
// found in the LICENSE file.
 #include "components/sync/engine/sync_manager_factory.h"
 
 >>> 
#include "components/sync/engine/sync_manager_impl.h"

 ... 
```
### patch
```cpp
#include "brave/components/sync/engine/brave_sync_manager_impl.h"

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 std::unique_ptr<SyncManager> SyncManagerFactory::CreateSyncManager(
    const std::string& name) { ... 
>>> 
 return std::make_unique<SyncManagerImpl>(name, network_connection_tracker_); 
<<< 
...} ...  } ...  
```
### patch
```cpp
  return std::make_unique<BraveSyncManagerImpl>(name, network_connection_tracker_);

```

