### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/password_manager/factories/password_store_backend_factory.h"

 ... 
```
### patch
```cpp
#if BUILDFLAG(IS_ANDROID)
#include "components/password_manager/core/browser/password_store/login_database.h"
#include "components/password_manager/core/browser/password_store/password_store_built_in_backend.h"
#endif  // BUILDFLAG(IS_ANDROID)

```

### match
```cpp
...
>>>
 CreatePasswordStoreBackend 
 ( 
 password_manager::IsAccountStore is_account_store 
 ,  <<< 
const base::FilePath& login_db_directory
 ... ) ...  
```
### patch
```cpp
CreatePasswordStoreBackend_ChromiumImpl(password_manager::IsAccountStore is_account_store,

```

### match
```cpp
...
 
 std::unique_ptr<password_manager::PasswordStoreBackend>
CreatePasswordStoreBackend_ChromiumImpl(password_manager::IsAccountStore is_account_store,
const base::FilePath& login_db_directory,
                           PrefService* prefs,
                           os_crypt_async::OSCryptAsync* os_crypt_async) { ... 
// BUILDFLAG(IS_ANDROID)
 } 
 >>> 
 ... 
```
### patch
```cpp
std::unique_ptr<password_manager::PasswordStoreBackend>
CreatePasswordStoreBackend(password_manager::IsAccountStore is_account_store,
                           const base::FilePath& login_db_directory,
                           PrefService* prefs,
                           os_crypt_async::OSCryptAsync* os_crypt_async) {
#if BUILDFLAG(IS_ANDROID)
  std::unique_ptr<password_manager::LoginDatabase> login_db(
      password_manager::CreateLoginDatabase(is_account_store,
                                            login_db_directory, prefs));
  auto behavior = is_account_store
                      ? syncer::WipeModelUponSyncDisabledBehavior::kAlways
                      : syncer::WipeModelUponSyncDisabledBehavior::kNever;
  return std::make_unique<password_manager::PasswordStoreBuiltInBackend>(
      std::move(login_db), behavior, prefs, os_crypt_async);
#else
  return CreatePasswordStoreBackend_ChromiumImpl(
      is_account_store, login_db_directory, prefs, os_crypt_async);
#endif
}
```

