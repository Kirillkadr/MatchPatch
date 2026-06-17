### match
```cpp
...
 #include <memory>
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/gtest_prod_util.h"

```

### match
```cpp
...
 #include "components/ukm/ukm_reporting_service.h"
 
 >>> 
 ... 
```
### patch
```cpp
class ChromeMetricsServiceClientTest;
class BraveTestRegisterUKMProviders;

```

### match
```cpp
...
 class PrefService 
 ; 
 >>> 
 ... 
```
### patch
```cpp
FORWARD_DECLARE_TEST(ChromeMetricsServiceClientTest,
                     BraveTestRegisterUKMProviders);

```

### match
```cpp
...
 
 namespace ukm { ... 
// cloned.
 base::CallbackListSubscription cloned_install_subscription_; 
 >>> 
 ... } ...  
```
### patch
```cpp
  FRIEND_TEST_ALL_PREFIXES(::ChromeMetricsServiceClientTest,
                           BraveTestRegisterUKMProviders);

```

