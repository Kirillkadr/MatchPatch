### match
```cpp
...
 #define COMPONENTS_SYNC_ENGINE_SYNC_SCHEDULER_H_
 
 >>> 
#include "base/compiler_specific.h"

 ...
```
### patch
```cpp
#include "components/sync/engine/sync_protocol_error.h"

```

### match
```cpp
...

 >>> 
virtual void OnCredentialsUpdated() = 0;
 ...
```
### patch
```cpp
virtual void SchedulePermanentlyDeleteAccount(                                   
      base::OnceCallback<void(const SyncProtocolError&)> callback) {}

```

