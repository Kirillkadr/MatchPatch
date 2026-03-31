### match
```cpp
...
// found in the LICENSE file.
 #include "components/history/core/browser/features.h"
 
 >>> 
#include "build/build_config.h"

 ...
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
BASE_FEATURE(kHistoryDatabaseWriteAheadLogging,
             base::FEATURE_DISABLED_BY_DEFAULT);
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kOrganicRepeatableQueries, base::FEATURE_DISABLED_BY_DEFAULT},
}});

BASE_FEATURE(kHistoryMoreSearchResults,
             base::FEATURE_DISABLED_BY_DEFAULT);

```

