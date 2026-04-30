### match
```cpp
...
#include "components/sync_user_events/user_event_service.h"

 #include "components/variations/service/google_groups_manager.h"
 
 >>> 
#if !BUILDFLAG(IS_ANDROID)
#include "components/webauthn/core/browser/passkey_data_type_controller.h"
#include "components/webauthn/core/browser/passkey_model.h"
#endif
 ... 
```
### patch
```cpp
#include "brave/components/history/core/browser/sync/brave_history_data_type_controller.h"
#include "brave/components/history/core/browser/sync/brave_history_delete_directives_data_type_controller.h"

```

### match
```cpp
...
 
 namespace browser_sync { ... 
 
 std::unique_ptr<syncer::DataTypeController>
CommonControllerBuilder::CreateHistoryDataTypeController(
    syncer::SyncService* sync_service) { ...   >>> 
 return 
 std::make_unique<history::HistoryDataTypeController> 
 (  <<<  ...) ...  } ...  } ...  
```
### patch
```cpp
  return std::make_unique<history::BraveHistoryDataTypeController>(

```

### match
```cpp
...
 
 namespace browser_sync { ... 
 
 std::unique_ptr<syncer::DataTypeController>
CommonControllerBuilder::CreateHistoryDeleteDirectivesDataTypeController(
    syncer::SyncService* sync_service,
    version_info::Channel channel) { ...   >>> 
 return 
 std::make_unique<history::HistoryDeleteDirectivesDataTypeController> 
 (  <<< 
base::BindRepeating(&syncer::ReportUnrecoverableError, channel)
 ... ) ...  } ...  } ...  
```
### patch
```cpp
  return std::make_unique<history::BraveHistoryDeleteDirectivesDataTypeController>(

```

