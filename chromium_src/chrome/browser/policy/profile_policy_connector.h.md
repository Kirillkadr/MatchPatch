### match
```cpp
...
 
 # ifndef ... 
#include "components/policy/core/common/policy_namespace.h"

 #include "components/policy/core/common/policy_service.h"
 
 >>> 
#if BUILDFLAG(IS_ANDROID)
#include "chrome/browser/ui/android/tab_model/tab_model_observer.h"
#else
#include "chrome/browser/ui/browser_list_observer.h"
#include "chrome/browser/ui/tabs/tab_strip_model_observer.h"
#endif
 ... 
```
### patch
```cpp
#include "components/policy/core/common/policy_service_impl.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace policy { ... 
// providers to inactive.
 void UseLocalTestPolicyProvider(); 
 >>> 
// Reverts the effects of UseLocalTestPolicyProvider.
 ... } ...  
```
### patch
```cpp
  raw_ptr<policy::ConfigurationPolicyProvider> GetBraveProfilePolicyProvider();

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace policy { ... 
std::unique_ptr<bool> is_managed_override_;
 raw_ptr<ConfigurationPolicyProvider> local_test_policy_provider_ = nullptr; 
 >>> 
std::unique_ptr<internal::LocalTestInfoBarVisibilityManager>
      local_test_infobar_visibility_manager_;
 ... } ...  
```
### patch
```cpp
  raw_ptr<policy::ConfigurationPolicyProvider> brave_profile_policy_provider_ = nullptr;

```

