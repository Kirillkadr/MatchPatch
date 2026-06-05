### match
```cpp
...
#include <optional>

 #include <string>
 
 >>> 
#include "base/cancelable_callback.h"

 ... 
```
### patch
```cpp
#include "components/sync/engine/sync_protocol_error.h"

```

### match
```cpp
...
 namespace 
 syncer 
 { 
 >>> 
class BackoffDelayProvider
 ... } ...  
```
### patch
```cpp
inline constexpr char kNigoriFolderNotReadyError[] =
    "nigori root folder entity is not ready yet";

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 class SyncSchedulerImpl : public SyncScheduler { ... 
void HandleFailure(const ModelNeutralState& model_neutral_state);
 // Invoke the Syncer to perform a poll job. 
 >>> 
void DoPollSyncCycleJob();
 ... } ...  } ...  
```
### patch
```cpp
  void HandleBraveConfigurationFailure(                                           
      const ModelNeutralState& model_neutral_state);
  void SchedulePermanentlyDeleteAccount(
      base::OnceCallback<void(const SyncProtocolError&)> callback) override;
  void PermanentlyDeleteAccountImpl(
      base::OnceCallback<void(const SyncProtocolError&)> callback);

```

