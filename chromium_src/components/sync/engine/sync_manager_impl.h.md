### match
```cpp
...
#include <string>

 #include <vector>
 
 >>> 
#include "base/functional/callback_forward.h"

 ... 
```
### patch
```cpp
#include "components/sync/engine/sync_manager.h"

```

### match
```cpp
...
 
 namespace syncer { ... 
void AddObserver(SyncManager::Observer* observer) override;
 void RemoveObserver(SyncManager::Observer* observer) override; 
 >>> 
void ShutdownOnSyncThread() override;
 ... } ...  
```
### patch
```cpp
  friend class BraveSyncManagerImpl;

```

