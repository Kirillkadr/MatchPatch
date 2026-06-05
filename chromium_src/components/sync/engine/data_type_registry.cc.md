### match
```cpp
...
#include "components/sync/engine/data_type_registry.h"

>>> 
 #include "brave/components/sync/engine/brave_data_type_worker.h"
 
<<< 
#include <stddef.h>

 ... 
```
### patch
```cpp

```

### match
```cpp
...
>>>
 auto 
 worker 
 = 
 std::make_unique<BraveDataTypeWorker> 
 ( 
<<< 
...) ...  
```
### patch
```cpp
  auto worker = std::make_unique<DataTypeWorker>(

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void DataTypeRegistry::ConnectDataType(
    DataType type,
    std::unique_ptr<DataTypeActivationResponse> activation_response) { ... 
// Save a raw pointer and add the worker to our structures.
>>> 
 BraveDataTypeWorker* worker_ptr = worker.get(); 
<<< 
connected_data_type_workers_.push_back(std::move(worker));
 ... } ...  } ...  
```
### patch
```cpp
  DataTypeWorker* worker_ptr = worker.get();

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 DataTypeSet DataTypeRegistry::GetConnectedTypes() const { ... 
>>> 
 for 
 ( 
 const 
 std::unique_ptr<BraveDataTypeWorker> 
 & worker 
 : 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  for (const std::unique_ptr<DataTypeWorker>& worker :

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 bool DataTypeRegistry::HasUnsyncedItems() const { ... 
>>> 
 for 
 ( 
 const 
 std::unique_ptr<BraveDataTypeWorker> 
 & worker 
 : 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  for (const std::unique_ptr<DataTypeWorker>& worker :

```

### match
```cpp
...
 
 namespace syncer { ... 
>>> 
 const 
 std::vector<std::unique_ptr<BraveDataTypeWorker>> 
 & 
<<< 
...} ...  
```
### patch
```cpp
const std::vector<std::unique_ptr<DataTypeWorker>>&

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void DataTypeRegistry::OnEncryptedTypesChanged(DataTypeSet encrypted_types,
                                               bool encrypt_everything) { ... 
>>> 
 for 
 ( 
 const 
 std::unique_ptr<BraveDataTypeWorker> 
 & worker 
 : 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  for (const std::unique_ptr<DataTypeWorker>& worker :

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void DataTypeRegistry::OnCryptographerStateChanged(Cryptographer* cryptographer,
                                                   bool has_pending_keys) { ... 
>>> 
 for 
 ( 
 const 
 std::unique_ptr<BraveDataTypeWorker> 
 & worker 
 : 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  for (const std::unique_ptr<DataTypeWorker>& worker :

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void DataTypeRegistry::OnPassphraseTypeChanged(PassphraseType type,
                                               base::Time passphrase_time) { ... 
>>> 
 for 
 ( 
 const 
 std::unique_ptr<BraveDataTypeWorker> 
 & worker 
 : 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  for (const std::unique_ptr<DataTypeWorker>& worker :

```

