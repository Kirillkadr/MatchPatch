### match
```cpp
...
#include <optional>

 #include <string>
 
 >>> 
#include "base/functional/bind.h"

 ... 
```
### patch
```cpp
#include <utility>
#include <vector>

```

### match
```cpp
...
 
 namespace signin { ... 
>>> 
 AccountsInCookieJarInfo 
 IdentityManager::GetAccountsInCookieJar() const 
 { 
<<< 
return gaia_cookie_manager_service_->ListAccounts();
 ... } ...  } ...  
```
### patch
```cpp
AccountsInCookieJarInfo IdentityManager::GetAccountsInCookieJar_Unused() const {

```

### match
```cpp
...
 
 namespace signin { ... 
 
 std::optional<size_t> IdentityManager::GetSessionIndexForPrimaryAccount()
    const { ... 
if (primary_account_info.gaia.empty()) {
    return std::nullopt;
  }
>>> 
 AccountsInCookieJarInfo accounts_in_cookie_jar = GetAccountsInCookieJar(); 
<<< 
const std::vector<gaia::ListedAccount>& accounts =
      accounts_in_cookie_jar.GetAllAccounts();
 ... } ...  } ...  
```
### patch
```cpp
  AccountsInCookieJarInfo accounts_in_cookie_jar = GetAccountsInCookieJar_Unused();

```

### match
```cpp
...
 
 namespace signin { ... 
>>> 
 void 
 IdentityManager::PrepareForAddingNewAccount() 
 { 
<<< 
account_fetcher_service_->PrepareForFetchingAccountCapabilities();
 ... } ...  } ...  
```
### patch
```cpp
void IdentityManager::PrepareForAddingNewAccount_Unused() {

```

### match
```cpp
...
 
 namespace signin { ... 
void IdentityManager::FireOnEndBatchOfPrimaryAccountChanges() {
  CHECK(!batch_of_primary_account_changes_in_progress_,
        base::NotFatalUntil::M140);
  for (auto& observer : observer_list_) {
    observer.OnEndBatchOfPrimaryAccountChanges();
  }
}
 #endif 
 // BUILDFLAG(IS_IOS) 
 >>> 
 ... } ...  
```
### patch
```cpp
AccountsInCookieJarInfo IdentityManager::GetAccountsInCookieJar() const {
  // accounts_in_cookie_jar_info.accounts_are_fresh must be false,
  // see `SyncServiceImpl::OnEngineInitialized`
  return AccountsInCookieJarInfo(/*accounts_are_fresh=*/false,
                                 std::vector<gaia::ListedAccount>());
}

void IdentityManager::PrepareForAddingNewAccount() {}

```

