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
#include "base/functional/callback_forward.h"
// chromium_src/components/sync/engine/sync_engine.h also redefines
// DisableProtocolEventForwarding include explicitly it to avoid compilation
// error 'DisableProtocolEventForwarding' macro redefined
#include "components/sync/engine/sync_engine.h"
#include "components/sync/engine/sync_protocol_error.h"

```

### match
```cpp
...
 
 namespace syncer { ... 
void GetThrottledDataTypesForTest(
      base::OnceCallback<void(DataTypeSet)> cb) const override;
 void RequestBufferedProtocolEventsAndEnableForwarding() override; 
 >>> 
void DisableProtocolEventForwarding() override;
 ... } ...  
```
### patch
```cpp
  void PermanentlyDeleteAccount(                                                  
      base::OnceCallback<void(const SyncProtocolError&)> callback) override;

```

