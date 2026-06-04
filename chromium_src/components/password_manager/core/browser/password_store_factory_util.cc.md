### match
```cpp
...
#include "components/password_manager/core/common/password_manager_pref_names.h"

 #include "components/prefs/pref_service.h"
 
 >>> 
#if !BUILDFLAG(IS_ANDROID)
#include "components/password_manager/core/browser/password_store/login_database.h"
#endif
 ... 
```
### patch
```cpp
#include "build/build_config.h"
#if BUILDFLAG(IS_ANDROID)
#include "components/password_manager/core/browser/password_store/login_database.h"
#endif  // !BUILDFLAG(IS_ANDROID)

```

### match
```cpp
...
 
 namespace password_manager { ... 
 
 void SanitizeAndMigrateCredentials(
    password_manager::CredentialsCleanerRunner* cleaning_tasks_runner,
    scoped_refptr<password_manager::PasswordStoreInterface> store,
    password_manager::IsAccountStore is_account_store,
    PrefService* prefs,
    base::TimeDelta delay,
    base::RepeatingCallback<network::mojom::NetworkContext*()>
        network_context_getter) { ... 
if (cleaning_tasks_runner->HasPendingTasks()) {
    // The runner will delete itself once the clearing tasks are done, thus we
    // are releasing ownership here.
    base::SequencedTaskRunner::GetCurrentDefault()->PostDelayedTask(
        FROM_HERE,
        base::BindOnce(
            &password_manager::CredentialsCleanerRunner::StartCleaning,
            cleaning_tasks_runner->GetWeakPtr()),
        delay);
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
#if BUILDFLAG(IS_ANDROID)
LoginDatabase::DeletingUndecryptablePasswordsEnabled GetPolicyFromPrefs(
    PrefService* prefs) {
  return LoginDatabase::DeletingUndecryptablePasswordsEnabled(true);
}
#endif  // BUILDFLAG(IS_ANDROID)

}  // namespace

```

