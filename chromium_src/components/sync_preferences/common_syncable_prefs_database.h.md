### match
```cpp
...
 #include <string_view>
 
 >>> 
 ... 
```
### patch
```cpp
#include <optional>
#include "components/sync_preferences/syncable_prefs_database.h"

```

### match
```cpp
...
 
 namespace sync_preferences { ... 
// syncable.
>>> 
 std::optional<SyncablePrefMetadata> GetSyncablePrefMetadata(
      std::string_view pref_name) const override; 
<<< 
...} ...  
```
### patch
```cpp
  std::optional<SyncablePrefMetadata> GetSyncablePrefMetadata_ChromiumImpl(std::string_view pref_name) const;
  std::optional<sync_preferences::SyncablePrefMetadata>
      GetSyncablePrefMetadata_ChromiumOriginalImpl(std::string_view pref_name) const;
  std::optional<sync_preferences::SyncablePrefMetadata>
  GetSyncablePrefMetadata(std::string_view pref_name) const override;

```

