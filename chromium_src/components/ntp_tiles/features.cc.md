### match
```cpp
...
// found in the LICENSE file.
 #include "components/ntp_tiles/features.h"
 
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
const base::FeatureParam<int> kPopularSitesRefreshUsArm{&kPopularSitesRefreshUs,
                                                        "arm", 0};
 >>> 
 ...
```
### patch
```cpp
// Disables fetching suggested web sites favicons
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kPopularSitesBakedInContentFeature, base::FEATURE_DISABLED_BY_DEFAULT},
    {kNtpMostLikelyFaviconsFromServerFeature,
     base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

