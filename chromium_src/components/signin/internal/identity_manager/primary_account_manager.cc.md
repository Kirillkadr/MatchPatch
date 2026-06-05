### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/signin/internal/identity_manager/primary_account_manager.h"

 ... 
```
### patch
```cpp
#include "components/signin/internal/identity_manager/primary_account_manager.h"

```

### match
```cpp
...
>>>
 void 
 PrimaryAccountManager::RevokeSyncConsent 
 ( 
<<< 
signin_metrics::ProfileSignout signout_source_metric
 ... ) ...  
```
### patch
```cpp
void PrimaryAccountManager::RevokeSyncConsent_ChromiumImpl(

```

### match
```cpp
...
 
 void PrimaryAccountManager::OnRefreshTokensLoaded() { ... 
#if !BUILDFLAG(IS_ANDROID)
  // Remove account information from the account tracker service if needed.
  if (token_service_->HasLoadCredentialsFinishedWithNoErrors()) {
    std::vector<AccountInfo> accounts_in_tracker_service =
        account_tracker_service_->GetAccounts();
    const CoreAccountId primary_account_id_ =
        GetPrimaryAccountId(signin::ConsentLevel::kSignin);
    for (const auto& account : accounts_in_tracker_service) {
      if (primary_account_id_ != account.account_id &&
          !token_service_->RefreshTokenIsAvailable(account.account_id)) {
        VLOG(0) << "Removed account from account tracker service: "
                << account.account_id;
        account_tracker_service_->RemoveAccount(account.account_id);
      }
    }
  }
#endif
 } 
 >>> 
 ... 
```
### patch
```cpp
void PrimaryAccountManager::RevokeSyncConsent(
    signin_metrics::ProfileSignout source_metric) {}

```

