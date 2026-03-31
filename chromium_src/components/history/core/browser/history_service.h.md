### match
```cpp
...
 
 # ifndef ... 
#include "sql/init_status.h"

 #include "ui/base/page_transition_types.h"
 
 >>> 
class GURL
 ...
```
### patch
```cpp
class BraveHistoryURLProviderTest;
class BraveHistoryQuickProviderTest;

```

### match
```cpp
...
 
// Updates the history database with the related searches for the Google SRP
 // visit. 
 >>> 
 ...
```
### patch
```cpp
  void GetKnownToSyncCount(                                                 
      base::OnceCallback<void(history::HistoryCountResult)> callback);

```

### match
```cpp
...
  void Cleanup(); 
 >>>
...
```
### patch
```cpp
  friend class ::BraveHistoryURLProviderTest;
  friend class ::BraveHistoryQuickProviderTest;
  void CleanupUnused();

```

