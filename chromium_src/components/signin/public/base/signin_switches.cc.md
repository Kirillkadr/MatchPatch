### match
```cpp
...
// found in the LICENSE file.
 #include "components/signin/public/base/signin_switches.h"
 
 >>> 
#include "base/feature_list.h"

 ...
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
BASE_FEATURE(kUsePrimaryAndTonalButtonsForPromos,
             base::FEATURE_ENABLED_BY_DEFAULT);

// keep-sorted end
 >>> 
 ... } ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kSyncEnableBookmarksInTransportMode, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

