### match
```cpp
...
 
 # ifndef ... 
#import "base/memory/raw_ptr.h"

 #import "components/policy/core/common/local_test_policy_provider.h"
 
 >>> 
class BrowserPolicyConnectorIOS
 ... 
```
### patch
```cpp
// Don't apply the renames to these files
#include "components/policy/core/common/policy_service_impl.h"

```

### match
```cpp
...
 
 # ifndef ... 
// providers to inactive.
 void UseLocalTestPolicyProvider(); 
 >>> 
// Reverts the effects of UseLocalTestPolicyProvider.
 ... 
```
### patch
```cpp
  raw_ptr<policy::ConfigurationPolicyProvider> GetBraveProfilePolicyProvider();

```

### match
```cpp
...
 
 # ifndef ... 
// profile.
 base::flat_set<std::string> GetUserAffiliationIds() const; 
 >>> 
private
 ... 
```
### patch
```cpp
// Add in brave_profile_policy_provider_ so we can pass it the profile ID

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ProfilePolicyConnector { ... 
 friend class ProfilePolicyConnectorMock; 
 >>> 
// `policy_providers_` contains a list of the policy providers available for
 ... } ...  
```
### patch
```cpp
  std::unique_ptr<policy::ConfigurationPolicyProvider>
      brave_profile_policy_provider_;

```

