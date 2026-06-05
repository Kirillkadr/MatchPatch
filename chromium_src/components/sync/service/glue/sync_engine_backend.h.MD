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
// chromium_src/components/sync/engine/sync_engine.h also redefines
// DisableProtocolEventForwarding include explicitly it to avoid compilation
// 'DisableProtocolEventForwarding' macro redefined
#include "components/sync/engine/sync_engine.h"

```

### match
```cpp
...
 namespace 
 syncer 
 { 
 >>> 
class CustomPassphraseBootstrapToken
 ... } ...  
```
### patch
```cpp
struct SyncProtocolError;

```

### match
```cpp
...
 
 namespace syncer { ... 
void DoFinishConfigureDataTypes(
      DataTypeSet types_to_config,
      base::OnceCallback<void(DataTypeSet, DataTypeSet)> ready_task);
 void SendBufferedProtocolEventsAndEnableForwarding(); 
 >>> 
void DisableProtocolEventForwarding();
 ... } ...  
```
### patch
```cpp
  void PermanentlyDeleteAccount(                                         
      base::OnceCallback<void(const SyncProtocolError&)> callback);

```

