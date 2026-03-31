### match
```cpp
...
#include "base/task/sequenced_task_runner.h"

 #include "base/threading/scoped_blocking_call.h"
 
 >>> 
#include "build/chromeos_buildflags.h"

 ... 
```
### patch
```cpp
#include "brave/components/constants/pref_names.h"
#include "build/build_config.h"

```

### match
```cpp
...
#include "chrome/common/buildflags.h"

 #include "chrome/common/chrome_constants.h"
 
 >>> 
#include "chrome/grit/branded_strings.h"

 ... 
```
### patch
```cpp
#include "chrome/common/pref_names.h"

```

### match
```cpp
...
#include "components/pref_registry/pref_registry_syncable.h"

 #include "components/prefs/pref_value_store.h"
 
 >>> 
#include "components/supervised_user/core/browser/family_link_settings_service.h"

 ... 
```
### patch
```cpp
#include "components/signin/public/base/signin_pref_names.h"
#include "components/spellcheck/browser/pref_names.h"

```

### match
```cpp
...
#include "services/preferences/public/mojom/tracked_preference_validation_delegate.mojom.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
namespace {

// Text content of README file created in each profile directory. Both %s
// placeholders must contain the product name. This is not localizable and hence
// not in resources.
const char kReadmeText[] =
    "%s settings and storage represent user-selected preferences and "
    "information and MUST not be extracted, overwritten or modified except "
    "through %s defined APIs.";

}
 ... 
```
### patch
```cpp
#include "ui/color/system_theme.h"


```

### match
```cpp
...
>>>
 void 
 RegisterProfilePrefs 
 ( 
 bool is_signin_profile 
 ,  <<< 
const std::string& locale
 ... ) ...  
```
### patch
```cpp
void RegisterProfilePrefs_ChromiumImpl(bool is_signin_profile,

```

### match
```cpp
...
 
 std::unique_ptr<sync_preferences::PrefServiceSyncable> CreateProfilePrefService(
    scoped_refptr<user_prefs::PrefRegistrySyncable> pref_registry,
    scoped_refptr<PrefStore> extension_pref_store,
    policy::PolicyService* policy_service,
    policy::ChromeBrowserPolicyConnector* browser_policy_connector,
    mojo::PendingRemote<prefs::mojom::TrackedPreferenceValidationDelegate>
        pref_validation_delegate,
    scoped_refptr<base::SequencedTaskRunner> io_task_runner,
    SimpleFactoryKey* key,
    const base::FilePath& profile_path,
    bool async_prefs,
    os_crypt_async::OSCryptAsync* os_crypt_async,
    supervised_user::DeviceParentalControls& device_parental_controls) { ... 
return chrome_prefs::CreateProfilePrefs(
      profile_path, std::move(pref_validation_delegate), policy_service,
      family_link_settings_service, device_parental_controls,
      std::move(extension_pref_store), pref_registry, browser_policy_connector,
      async_prefs, io_task_runner, os_crypt_async);
 } 
 >>> 
 ... 
```
### patch
```cpp
// Prefs for KeyedService
void RegisterProfilePrefs(bool is_signin_profile,
                          const std::string& locale,
                          user_prefs::PrefRegistrySyncable* registry) {
  RegisterProfilePrefs_ChromiumImpl(is_signin_profile, locale, registry);

  // Change default pref values that are registered by keyed services

  // Disable spell check service
  registry->SetDefaultPrefValue(
      spellcheck::prefs::kSpellCheckUseSpellingService, base::Value(false));

  registry->SetDefaultPrefValue(prefs::kSigninAllowedOnNextStartup,
                                base::Value(false));
#if BUILDFLAG(IS_LINUX)
  // Use brave theme by default instead of gtk theme.
  registry->SetDefaultPrefValue(
      prefs::kSystemTheme,
      base::Value(static_cast<int>(ui::SystemTheme::kDefault)));
#endif
}
```

