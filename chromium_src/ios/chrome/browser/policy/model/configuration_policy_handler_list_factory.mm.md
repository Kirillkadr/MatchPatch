### match
```cpp
...
#import "ios/chrome/browser/policy/model/configuration_policy_handler_list_factory.h"

 #import <array>
 
 >>> 
#import "base/check.h"

 ... 
```
### patch
```cpp
#include "ios/chrome/browser/policy/model/configuration_policy_handler_list_factory.h"
#include <memory>

```

### match
```cpp
...
>>>
 std::unique_ptr<policy::ConfigurationPolicyHandlerList> 
 BuildPolicyHandlerList 
 (  <<< 
bool are_future_policies_allowed_by_default
 ... ) ...  
```
### patch
```cpp
std::unique_ptr<policy::ConfigurationPolicyHandlerList> BuildPolicyHandlerList_ChromiumImpl(

```

### match
```cpp
...
 
 std::unique_ptr<policy::ConfigurationPolicyHandlerList> BuildPolicyHandlerList_ChromiumImpl(
bool are_future_policies_allowed_by_default,
    const policy::Schema& chrome_schema) { ... 
return handlers;
 } 
 >>> 
 ... 
```
### patch
```cpp
namespace brave {
std::unique_ptr<policy::ConfigurationPolicyHandlerList> BuildPolicyHandlerList(
    std::unique_ptr<policy::ConfigurationPolicyHandlerList> handlers);
}

std::unique_ptr<policy::ConfigurationPolicyHandlerList> BuildPolicyHandlerList(
    bool are_future_policies_allowed_by_default,
    const policy::Schema& chrome_schema) {
  std::unique_ptr<policy::ConfigurationPolicyHandlerList> handlers =
      BuildPolicyHandlerList_ChromiumImpl(
          are_future_policies_allowed_by_default, chrome_schema);
  return brave::BuildPolicyHandlerList(std::move(handlers));
}
```

