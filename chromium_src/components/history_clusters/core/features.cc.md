### match
```cpp
...
// found in the LICENSE file.
 #include "components/history_clusters/core/features.h"
 
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
 
 namespace history_clusters { ... 
 
 BASE_FEATURE ( ... 
kSearchesFindUngroupedVisits,
             "GroupedHistorySearchesFindUngroupedVisits",
             
 base::FEATURE_ENABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kHistoryClustersInternalsPage, base::FEATURE_DISABLED_BY_DEFAULT},
    {kHistoryClustersNavigationContextClustering,
     base::FEATURE_DISABLED_BY_DEFAULT},
    {kJourneys, base::FEATURE_DISABLED_BY_DEFAULT},
    {kJourneysImages, base::FEATURE_DISABLED_BY_DEFAULT},
    {kOmniboxHistoryClusterProvider, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

