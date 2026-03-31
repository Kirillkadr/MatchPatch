### match
```cpp
...
#include <list>

 #include <utility>
 
 >>> 
#include "base/no_destructor.h"

 ... 
```
### patch
```cpp
#include "base/files/file_path.h"

```

### match
```cpp
...
#else  // Non-ChromeOS.
#include "components/policy/core/common/cloud/cloud_policy_manager.h"

 #endif 
 >>> 
 ... 
```
### patch
```cpp
namespace brave_policy {
class BraveProfilePolicyProvider;
void SetBraveProfilePolicyProviderProfileID(
    policy::ConfigurationPolicyProvider* provider,
    const base::FilePath& profile_path);
}  // namespace brave_policy


```

### match
```cpp
...
>>>
 CreateProfilePolicyConnectorForBrowserContext 
 (  <<< 
SchemaRegistry* schema_registry
 ... ) ...  
```
### patch
```cpp
CreateProfilePolicyConnectorForBrowserContext_ChromiumImpl(

```

### match
```cpp
...
 
 namespace policy { ... 
 
 void PushProfilePolicyConnectorProviderForTesting(
    ConfigurationPolicyProvider* provider) { ... 
test_providers->push_back(provider);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
std::unique_ptr<ProfilePolicyConnector>
CreateProfilePolicyConnectorForBrowserContext(
    SchemaRegistry* schema_registry,
    CloudPolicyManager* cloud_policy_manager,
    ConfigurationPolicyProvider* policy_provider,
    policy::ChromeBrowserPolicyConnector* browser_policy_connector,
    bool force_immediate_load,
    content::BrowserContext* context) {
  auto connector = CreateProfilePolicyConnectorForBrowserContext_ChromiumImpl(
      schema_registry, cloud_policy_manager, policy_provider,
      browser_policy_connector, force_immediate_load, context);
  // Some upstream browser tests don't do the normal flow so have no provider
  if (connector->GetBraveProfilePolicyProvider()) {
    brave_policy::SetBraveProfilePolicyProviderProfileID(
        connector->GetBraveProfilePolicyProvider().get(), context->GetPath());
  }

  return connector;
}

```

