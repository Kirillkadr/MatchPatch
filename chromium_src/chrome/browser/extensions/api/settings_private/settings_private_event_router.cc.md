### match
```
...
#include "base/functional/callback_helpers.h"

 #include "base/task/single_thread_task_runner.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/browser/extensions/api/settings_private/brave_prefs_util.h"

```

### match
```
...
 
 namespace extensions { ... 
 
 SettingsPrivateEventRouter::SettingsPrivateEventRouter(
    content::BrowserContext* context)
    : context_(context) { ... 
Profile* profile = Profile::FromBrowserContext(context_);  >>> 
 prefs_util_ = std::make_unique<PrefsUtil>(profile);  <<< 
user_prefs_registrar_.Init(profile->GetPrefs());
 ... } ...  } ...  
```
### patch
```
  prefs_util_ = std::make_unique<BravePrefsUtil>(profile);

```

### match
```
...
 
 namespace extensions { ... 
 
 void SettingsPrivateEventRouter::Shutdown() { ... 
 
 if (listening_) { ... 
#if BUILDFLAG(IS_CHROMEOS)
    cros_settings_subscription_map_.clear();
#endif  >>> 
 const PrefsUtil::TypedPrefMap& keys = prefs_util_->GetAllowlistedKeys();  <<< 
settings_private::GeneratedPrefs* generated_prefs =
        settings_private::GeneratedPrefsFactory::GetForBrowserContext(context_);
 ... } ...  } ...  } ...  
```
### patch
```
    const BravePrefsUtil::TypedPrefMap& keys = prefs_util_->GetAllowlistedKeys();

```

### match
```
...
 
 namespace extensions { ... 
 
 void SettingsPrivateEventRouter::StartOrStopListeningForPrefsChanges() { ... 
 
 if (should_listen && !listening_) { ...   >>> 
 const PrefsUtil::TypedPrefMap& keys = prefs_util_->GetAllowlistedKeys();  <<< 
for (const auto& it : keys) {
      std::string pref_name = it.first;
      if (prefs_util_->IsCrosSetting(pref_name)) {
#if BUILDFLAG(IS_CHROMEOS)
        base::CallbackListSubscription subscription =
            ash::CrosSettings::Get()->AddSettingsObserver(
                pref_name.c_str(),
                base::BindRepeating(
                    &SettingsPrivateEventRouter::OnPreferenceChanged,
                    base::Unretained(this), pref_name));
        cros_settings_subscription_map_.insert(
            make_pair(pref_name, std::move(subscription)));
#endif
      } else if (generated_prefs && generated_prefs->HasPref(pref_name)) {
        generated_prefs->AddObserver(pref_name, this);
      } else {
        FindRegistrarForPref(it.first)->Add(
            pref_name, base::BindRepeating(
                           &SettingsPrivateEventRouter::OnPreferenceChanged,
                           base::Unretained(this)));
      }
    }
 ... } ...  } ...  } ...  
```
### patch
```
    const BravePrefsUtil::TypedPrefMap& keys = prefs_util_->GetAllowlistedKeys();

```

### match
```
...
 
 namespace extensions { ... 
 
 void SettingsPrivateEventRouter::StartOrStopListeningForPrefsChanges() { ... 
 
 if (!should_listen && listening_) { ...   >>> 
 const PrefsUtil::TypedPrefMap& keys = prefs_util_->GetAllowlistedKeys();  <<< 
for (const auto& it : keys) {
      if (prefs_util_->IsCrosSetting(it.first)) {
#if BUILDFLAG(IS_CHROMEOS)
        cros_settings_subscription_map_.erase(it.first);
#endif
      } else if (generated_prefs && generated_prefs->HasPref(it.first)) {
        generated_prefs->RemoveObserver(it.first, this);
      } else {
        FindRegistrarForPref(it.first)->Remove(it.first);
      }
    }
 ... } ...  } ...  } ...  
```
### patch
```
    const BravePrefsUtil::TypedPrefMap& keys = prefs_util_->GetAllowlistedKeys();

```

