### match
```cpp
...
// found in the LICENSE file.
 #include "components/history/core/browser/visit_database.h"
 
 >>> 
#include <stddef.h>

 ...
```
### patch
```cpp
#include "components/history/core/browser/history_types.h"

```

### match
```cpp
...
 
 namespace history { ... 
 
 namespace { ... 
 
 VisitSource VisitSourceFromInt(int value) { ... 
case SOURCE_FIREFOX_IMPORTED:
 case SOURCE_IE_IMPORTED: 
 >>> 
case SOURCE_SAFARI_IMPORTED:
 ... } ...  } ...  } ...
```
### patch
```cpp
    case SOURCE_CHROME_IMPORTED:
  case SOURCE_BRAVE_IMPORTED:

```

### match
```cpp
...
bool VisitDatabase::MigrateVisitsAddAppId() {
  if (!GetDB().DoesTableExist("visits")) {
    NOTREACHED() << " Visits table should exist before migration";
  }
  if (!GetDB().DoesColumnExist("visits", "app_id")) {
    if (!GetDB().Execute("ALTER TABLE visits ADD COLUMN app_id TEXT")) {
      return false;
    }
  }
  return true;
} 
 >>> 
 ...
```
### patch
```cpp
bool VisitDatabase::GetKnownToSyncCount(int* count) {
  sql::Statement statement(
      GetDB().GetCachedStatement(SQL_FROM_HERE,
                                 "SELECT COUNT(*) "
                                 "FROM visits "
                                 "WHERE is_known_to_sync == TRUE"));

  *count = 0;
  if (statement.Step()) {
    *count = statement.ColumnInt(0);
  }
  return true;
}

```

