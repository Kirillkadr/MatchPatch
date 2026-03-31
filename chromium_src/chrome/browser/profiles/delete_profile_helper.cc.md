### match
```cpp
...
#include "chrome/browser/profiles/delete_profile_helper.h"

 #include <memory>
 
 >>> 
#include "base/check.h"

 ...
```
### patch
```cpp
#include <string_view>

```

### match
```cpp
...
#include "base/logging.h"

 #include "base/task/thread_pool.h"
 
 >>> 
#include "build/build_config.h"

 ...
```
### patch
```cpp
#include "brave/components/sync/service/brave_sync_service_impl.h"

```

### match
```cpp
...
#include "components/signin/public/identity_manager/primary_account_mutator.h"

 #include "components/sync/service/sync_service.h"
 
 >>> 
#include "content/public/browser/browser_task_traits.h"

 ...
```
### patch
```cpp
#include "components/sync/service/sync_user_settings.h"

```

### match
```cpp
...
#include "content/public/browser/browser_task_traits.h"

 #include "content/public/browser/browser_thread.h"
 
 >>> 
namespace {

// Called after a deleted profile was checked and cleaned up.
void ProfileCleanedUp(base::Value profile_path_value) {
  if (!g_browser_process || g_browser_process->IsShuttingDown()) {
    return;
  }
  ScopedListPrefUpdate deleted_profiles(g_browser_process->local_state(),
                                        prefs::kProfilesDeleted);
  deleted_profiles->EraseValue(profile_path_value);
}

// Helper function that deletes entries from the kProfilesLastActive pref list.
// It is called when every ephemeral profile is handled.
void RemoveFromLastActiveProfilesPrefList(const base::FilePath& path) {
  PrefService* local_state = g_browser_process->local_state();
  DCHECK(local_state);
  ScopedListPrefUpdate update(local_state, prefs::kProfilesLastActive);
  base::ListValue& profile_list = update.Get();
  base::Value entry_value = base::Value(path.BaseName().AsUTF8Unsafe());
  profile_list.EraseValue(entry_value);
}

bool IsRegisteredAsEphemeral(ProfileAttributesStorage* storage,
                             const base::FilePath& profile_dir) {
  ProfileAttributesEntry* entry =
      storage->GetProfileAttributesWithPath(profile_dir);
  return entry && entry->IsEphemeral();
}

// Disables sync in order to prevent that browsing data deletions propagate
// across devices via sync.
void DisableSyncForProfileDeletion(Profile* profile) {
  signin::IdentityManager* identity_manager =
      IdentityManagerFactory::GetForProfileIfExists(profile);
  if (!identity_manager ||
      !identity_manager->HasPrimaryAccount(signin::ConsentLevel::kSignin)) {
    // Nothing to do as the user is signed out (hence sync is guaranteed to be
    // disabled).
    return;
  }

#if BUILDFLAG(IS_CHROMEOS)
  // On ChromeOS, profile deletion uses a different codepath but some
  // browser tests do exercise this code.
  CHECK_IS_TEST();
#else
  identity_manager->GetPrimaryAccountMutator()->ClearPrimaryAccount(
      signin_metrics::ProfileSignout::kSignoutDuringProfileDeletion);
#endif  // BUILDFLAG(IS_CHROMEOS)
}

}
 ...
```
### patch
```cpp
class Profile;

```

### match
```cpp
...
 
 namespace { ... 
 void 
 DisableSyncForProfileDeletion(Profile* profile) 
 { 
 >>> 
signin::IdentityManager* identity_manager =
      IdentityManagerFactory::GetForProfileIfExists(profile);
 ... } ...  } ...
```
### patch
```cpp
signin::IdentityManager* identity_manager_unused = nullptr;
  (void)(identity_manager_unused);
  static_assert(std::string_view(__func__) == "DisableSyncForProfileDeletion",
                "Override at a wrong function");

```

### match
```cpp
...
  >>> 
 !identity_manager->HasPrimaryAccount(signin::ConsentLevel::kSignin) 
 ) 
 {  <<< ...
```
### patch
```cpp
!identity_manager->HasPrimaryAccount(signin::ConsentLevel::kSignin)&& StopSyncIfActive(profile, __func__)) {

```

### match
```cpp
...
#include <memory>

 #include <string_view>
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```cpp



```

### match
```cpp
...
 
 namespace { ... 
 
 void DisableSyncForProfileDeletion(Profile* profile) { ... 
// BUILDFLAG(IS_CHROMEOS)
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool StopSyncIfActive(Profile* profile, const char* func_name) {
  // If HasPrimaryAccount is used somewhere out of DisableSyncForProfileDeletion
  // we don't want to stop Sync.
  if (std::string_view(func_name) != "DisableSyncForProfileDeletion") {
    VLOG(0) << "Unexpected call of StopSyncIfActive from " << func_name
            << " Sync is not stopped";
    return true;
  }

  if (SyncServiceFactory::HasSyncService(profile)) {
    syncer::BraveSyncServiceImpl* sync_service =
        static_cast<syncer::BraveSyncServiceImpl*>(
            SyncServiceFactory::GetForProfile(profile));
    sync_service->StopAndClearWithShutdownReason();
  }

  return true;
}

```

### match
```cpp
...
 
 void DeleteProfileHelper::OnNewActiveProfileInitialized(
    const base::FilePath& profile_to_delete_path,
    const base::FilePath& new_active_profile_path,
    ProfileLoadedCallback callback,
    std::unique_ptr<ScopedKeepAlive> keep_alive,
    std::unique_ptr<ScopedProfileKeepAlive> profile_keep_alive,
    Profile* loaded_profile) { ... 
std::move(callback).Run(loaded_profile);
 } 
 >>> 
 ... 
```
### patch
```cpp
#pragma clang diagnostic pop
```

