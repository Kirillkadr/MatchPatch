### match
```cpp
...
 #define COMPONENTS_SIGNIN_INTERNAL_IDENTITY_MANAGER_PRIMARY_ACCOUNT_MUTATOR_IMPL_H_
 
 >>> 
#include "base/functional/callback.h"

 ...
```
### patch
```cpp
#include "components/signin/internal/identity_manager/primary_account_manager.h"
#include "components/signin/public/identity_manager/primary_account_mutator.h"

```

### match
```cpp
...
 
 namespace signin { ... 
 
PrimaryAccountError SetPrimaryAccount(
      const CoreAccountId& account_id,
      ConsentLevel consent_level,
      signin_metrics::AccessPoint access_point,
      base::OnceClosure prefs_committed_callback) override;
#if !BUILDFLAG(IS_CHROMEOS)
 >>> 
 ...
```
### patch
```cpp
void RevokeSyncConsent_ChromiumImpl(                    
      signin_metrics::ProfileSignout source_metric);

```

