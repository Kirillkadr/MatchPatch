### match
```cpp
...
// found in the LICENSE file.
 #include "components/omnibox/browser/aim_eligibility_service_features.h"
 
 >>> 
#include "base/metrics/field_trial_params.h"

 ...
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
const base::FeatureParam<base::TimeDelta> kAimEligibilityServiceDebounceDelay{
    &kAimEligibilityServiceDebounce, "delay", base::Milliseconds(100)};
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kAimEnabled, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

