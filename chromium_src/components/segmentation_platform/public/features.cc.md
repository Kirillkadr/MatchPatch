### match
```cpp
...
// found in the LICENSE file.
 #include "components/segmentation_platform/public/features.h"
 
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
 
constexpr base::FeatureParam<int>
    kNewTabPageCustomizationV2IphDisplayIntervalDays{
        &kNewTabPageCustomizationV2, "iph_display_interval_days",
        /*default_value=*/7};
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kSegmentationPlatformDeviceTier, base::FEATURE_DISABLED_BY_DEFAULT},
    {kSegmentationPlatformFeature, base::FEATURE_DISABLED_BY_DEFAULT},
    {kSegmentationPlatformTimeDelaySampling, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

