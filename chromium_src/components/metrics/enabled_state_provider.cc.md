### match
```cpp
...
 #define COMPONENTS_METRICS_ENABLED_STATE_PROVIDER_H_
 
 >>> 
namespace metrics {

// An interface that provides whether metrics should be reported.
class EnabledStateProvider {
 public:
  virtual ~EnabledStateProvider() = default;

  // Indicates that the user has provided consent to collect and report metrics.
  virtual bool IsConsentGiven() const = 0;

  // Should collection and reporting be enabled. This should depend on consent
  // being given.
  virtual bool IsReportingEnabled() const;

  // Enable or disable checking whether field trials are forced or not at
  // EnabledStateProvider::IsReportingEnabled().
  static void SetIgnoreForceFieldTrialsForTesting(bool ignore_trials);
};

}
 ... 
```
### patch
```cpp
#include "components/metrics/enabled_state_provider.h"
#include "base/base_switches.h"
#include "base/command_line.h"

```

### match
```cpp
...
 namespace 
 metrics 
 { 
 >>> 
// An interface that provides whether metrics should be reported.
 ... } ...  
```
### patch
```cpp
bool EnabledStateProvider::IsReportingEnabled() const {
  return false;
}

void EnabledStateProvider::SetIgnoreForceFieldTrialsForTesting(
    bool ignore_trials) {}

```

