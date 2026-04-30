### match
```cpp
...
// found in the LICENSE file.
 #include "components/metrics/metrics_features.h"
 
 >>> 
namespace metrics::features {

BASE_FEATURE(kStructuredMetrics,
             "EnableStructuredMetrics",
             base::FEATURE_ENABLED_BY_DEFAULT);

BASE_FEATURE(kFlushPersistentSystemProfileOnWrite,
             base::FEATURE_DISABLED_BY_DEFAULT);

BASE_FEATURE(kReportingServiceAlwaysFlush, base::FEATURE_DISABLED_BY_DEFAULT);

BASE_FEATURE(kMetricsLogTrimming, base::FEATURE_ENABLED_BY_DEFAULT);

#if BUILDFLAG(IS_ANDROID)
BASE_FEATURE(kMetricsLogJobSchedulerUpload, base::FEATURE_DISABLED_BY_DEFAULT);
#endif  // BUILDFLAG(IS_ANDROID)

// Enabled by default - intended as a kill-switch.
BASE_FEATURE(kPerProfileMetrics, base::FEATURE_ENABLED_BY_DEFAULT);

BASE_FEATURE(kRestructureMetricsConsentSettings,
             base::FEATURE_DISABLED_BY_DEFAULT);

BASE_FEATURE(kConsolidateMetricsServiceLocales,
             base::FEATURE_DISABLED_BY_DEFAULT);

}
 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 namespace metrics::features { ... 
 
 BASE_FEATURE ( ... 
kConsolidateMetricsServiceLocales,
             
 base::FEATURE_DISABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kStructuredMetrics, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

