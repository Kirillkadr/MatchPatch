### match
```cpp
...
#include <utility>

 #include <vector>
 
 >>> 
#include "base/command_line.h"

 ... 
```
### patch
```cpp
#include "brave/browser/policy/brave_simple_policy_map.h"
#include "brave/browser/policy/handlers/brave_adblock_policy_handler.h"
#include "brave/browser/policy/handlers/brave_fingerprinting_v2_policy_handler.h"
#include "brave/browser/policy/handlers/brave_https_upgrade_policy_handler.h"
#include "brave/browser/policy/handlers/brave_referrers_policy_handler.h"
#include "brave/browser/policy/handlers/brave_remember_1p_storage_policy_handler.h"

```

### match
```cpp
...
>>>
 std::unique_ptr<ConfigurationPolicyHandlerList> 
 BuildHandlerList 
 (  <<< 
const Schema& chrome_schema
 ... ) ...  
```
### patch
```cpp
std::unique_ptr<ConfigurationPolicyHandlerList> BuildHandlerList_ChromiumImpl(

```

### match
```cpp
...
 
 namespace policy { ... 
 
 std::unique_ptr<ConfigurationPolicyHandlerList> BuildHandlerList_ChromiumImpl(
const Schema& chrome_schema) { ... 
return handlers;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
std::unique_ptr<ConfigurationPolicyHandlerList> BuildHandlerList(
    const Schema& chrome_schema) {
  std::unique_ptr<ConfigurationPolicyHandlerList> handlers =
      BuildHandlerList_ChromiumImpl(chrome_schema);

  for (const auto& entry : kBraveSimplePolicyMap) {
    handlers->AddHandler(std::make_unique<SimplePolicyHandler>(
        entry.policy_name, entry.preference_path, entry.value_type));
  }

  handlers->AddHandler(std::make_unique<BraveAdblockPolicyHandler>());
  handlers->AddHandler(std::make_unique<BraveFingerprintingV2PolicyHandler>());
  handlers->AddHandler(std::make_unique<BraveHttpsUpgradePolicyHandler>());
  handlers->AddHandler(std::make_unique<BraveReferrersPolicyHandler>());
  handlers->AddHandler(std::make_unique<BraveRemember1PStoragePolicyHandler>());

  return handlers;
}

```

