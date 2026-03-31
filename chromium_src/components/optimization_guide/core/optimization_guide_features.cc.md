### match
```cpp
...
#include <cstring>

 #include <optional>
 
 >>> 
#include "base/byte_count.h"

 ...
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
std::optional<base::TimeDelta> GetMainFrameGetAIPageContentTimeout() {
  if (!base::FeatureList::IsEnabled(kGetAIPageContentMainFrameTimeoutEnabled)) {
    return std::nullopt;
  }
  return kGetAIPageContentMainFrameTimeoutParam.Get();
}
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kOptimizationGuideFetchingForSRP, base::FEATURE_DISABLED_BY_DEFAULT},
    {kOptimizationHints, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

