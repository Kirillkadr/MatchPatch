### match
```cpp
 ...
 >>>
 #import "base/containers/flat_set.h"
 ...
```
### patch
```cpp

#include "components/policy/core/browser/browser_policy_connector.h"
#include "components/policy/core/common/policy_service.h"

```

### match
```cpp

...
 >>> CreatePolicyProviders <<<
 ...
```
### patch
```cpp
  CreatePolicyProviders_ChromiumImpl();                             
  std::vector<std::unique_ptr<policy::ConfigurationPolicyProvider>> 
      CreatePolicyProviders


```

