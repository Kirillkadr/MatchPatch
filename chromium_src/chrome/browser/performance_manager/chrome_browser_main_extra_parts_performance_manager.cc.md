### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/performance_manager/public/chrome_browser_main_extra_parts_performance_manager.h"

 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)
#include "chrome/browser/performance_manager/metrics/metrics_provider_desktop.h"
namespace performance_manager::metrics {
namespace {
class StubGraphOwnedDefaultImpl : public GraphOwnedDefaultImpl {};
}  // namespace
}  // namespace performance_manager::metrics

namespace performance_manager {

class FakeMetricsProviderDesktop {
 public:
  static FakeMetricsProviderDesktop* GetInstance() {
    static FakeMetricsProviderDesktop instance;
    return &instance;
  }

  void Initialize() {
    // Do nothing
  }
};
}  // namespace performance_manager

#define PageResourceMonitor StubGraphOwnedDefaultImpl
#define MetricsProviderDesktop FakeMetricsProviderDesktop
#endif

```

### match
```cpp
...
 
 void ChromeBrowserMainExtraPartsPerformanceManager::OnProfileWillBeDestroyed(
    Profile* profile) { ... 
#if BUILDFLAG(IS_ANDROID)
  if (profile_discard_opt_out_list_helper_) {
    profile_discard_opt_out_list_helper_->OnProfileWillBeRemoved(profile);
  }
#else
  profile_discard_opt_out_list_helper_->OnProfileWillBeRemoved(profile);
#endif
 } 
 >>> 
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)
#undef MetricsProviderDesktop
#undef PageResourceMonitor
#endif  // !BUILDFLAG(IS_ANDROID)
```

