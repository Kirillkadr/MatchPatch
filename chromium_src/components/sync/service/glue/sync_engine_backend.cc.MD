### match
```cpp
...
// found in the LICENSE file.
 #include "components/sync/service/glue/sync_engine_backend.h"
 
 >>> 
#include <utility>

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
namespace {

constexpr base::FilePath::CharType kNigoriStorageFilename[] =
    FILE_PATH_LITERAL("Nigori.bin");

void RecordInvalidationPerDataType(DataType type) {
  UMA_HISTOGRAM_ENUMERATION("Sync.InvalidationPerDataType",
                            DataTypeHistogramValue(type));
}

void RecordIncomingInvalidationStatus(
    SyncEngineBackend::IncomingInvalidationStatus status) {
  UMA_HISTOGRAM_ENUMERATION("Sync.IncomingInvalidationStatus", status);
}

}
 ... } ...  
```
### patch
```cpp
void SyncEngineBackend::PermanentlyDeleteAccount(
    base::OnceCallback<void(const SyncProtocolError&)> callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  sync_manager_->PermanentlyDeleteAccount(std::move(callback));
}

```

