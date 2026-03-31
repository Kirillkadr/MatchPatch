### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/metrics/chrome_metrics_service_client.h"

 ... 
```
### patch
```cpp
#define ChromeMetricsServiceClient ChromeMetricsServiceClient_ChromiumImpl

```

### match
```cpp
...
 
 void ChromeMetricsServiceClient::CreateStructuredMetricsService() { ... 
if (recorder) {
    structured_metrics_service_ =
        std::make_unique<metrics::structured::StructuredMetricsService>(
            this, local_state, std::move(recorder));
    structured_metrics_service_->RegisterMetricsProvider(
        std::make_unique<variations::FieldTrialsProvider>(
            synthetic_trial_registry_, "StructuredMetrics"));
  }
 } 
 >>> 
 ... 
```
### patch
```cpp
#undef ChromeMetricsServiceClient
ChromeMetricsServiceClient::ChromeMetricsServiceClient(
    metrics::MetricsStateManager* state_manager,
    variations::SyntheticTrialRegistry* synthetic_trial_registry)
    : ChromeMetricsServiceClient_ChromiumImpl(state_manager,
                                              synthetic_trial_registry) {}

void ChromeMetricsServiceClient::RegisterMetricsServiceProviders() {
  // Do nothing.
}

void ChromeMetricsServiceClient::RegisterUKMProviders() {
  // Do nothing.
}
```

