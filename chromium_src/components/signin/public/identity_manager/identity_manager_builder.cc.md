### match
```cpp
...
#include <string>

 #include <utility>
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/signin/internal/identity_manager/brave_primary_account_mutator_impl.h"
#include "components/signin/public/identity_manager/identity_manager.h"

```

### match
```cpp
...
>>>
 IdentityManager::InitParameters 
 BuildIdentityManagerInitParameters 
 ( 
<<< 
IdentityManagerBuildParams* params
 ... ) ...  
```
### patch
```cpp
IdentityManager::InitParameters BuildIdentityManagerInitParameters_ChromiumImpl(

```

### match
```cpp
...
 
 namespace signin { ... 
 
 IdentityManager::InitParameters BuildIdentityManagerInitParameters_ChromiumImpl(
IdentityManagerBuildParams* params) { ... 
return init_params;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
std::unique_ptr<IdentityManager> BuildIdentityManager_Unused(
    IdentityManagerBuildParams* params) {
  return std::make_unique<IdentityManager>(
      BuildIdentityManagerInitParameters_ChromiumImpl(params));
}
IdentityManager::InitParameters BuildIdentityManagerInitParameters(
    IdentityManagerBuildParams* params) {
  IdentityManager::InitParameters init_params =
      BuildIdentityManagerInitParameters_ChromiumImpl(params);

  init_params.primary_account_mutator =
      std::make_unique<BravePrimaryAccountMutatorImpl>(
          init_params.account_tracker_service.get(),
          init_params.primary_account_manager.get(), params->pref_service,
          params->signin_client);

  return init_params;
}


```

