### match
```cpp
...
 
 # ifndef ... 
#include <vector>

 #include "base/containers/flat_set.h"
 
 >>> 
#include "base/memory/raw_ptr.h"

 ...
```
### patch
```cpp
#include "base/gtest_prod_util.h"

```

### match
```cpp
... 
 // BrowserPolicyConnectorBase:: 
 >>> 
std::vector<std::unique_ptr<policy::ConfigurationPolicyProvider>>
  CreatePolicyProviders() override;
...
```
### patch
```cpp
std::vector<std::unique_ptr<policy::ConfigurationPolicyProvider>>
  CreatePolicyProviders_ChromiumImpl();

```

