### match
```cpp
...
// found in the LICENSE file.
 #include "components/content_settings/core/browser/host_content_settings_map.h"
 
 >>> 
#include <stddef.h>

 ... 
```
### patch
```cpp
#include "brave/components/content_settings/core/browser/remote_list_provider.h"
#include "build/build_config.h"
#if !BUILDFLAG(IS_IOS)
#include "brave/components/content_settings/core/browser/brave_content_settings_pref_provider.h"
#endif

```

### match
```cpp
...
 
 HostContentSettingsMap::HostContentSettingsMap(PrefService* prefs,
                                               bool is_off_the_record,
                                               bool store_last_modified,
                                               bool restore_session,
                                               bool should_record_metrics)
    : RefcountedKeyedService(base::SingleThreadTaskRunner::GetCurrentDefault()),
#ifndef NDEBUG
      used_from_thread_id_(base::PlatformThread::CurrentId()),
#endif
      prefs_(prefs),
      is_off_the_record_(is_off_the_record),
      store_last_modified_(store_last_modified),
      allow_invalid_secondary_pattern_for_testing_(false),
      clock_(base::DefaultClock::GetInstance()) { ... 
user_modifiable_providers_.push_back(pref_provider_.get());
 pref_provider_->AddObserver(this); 
 >>> 
auto default_provider = std::make_unique<content_settings::DefaultProvider>(
      prefs_, is_off_the_record_, should_record_metrics);
 ... } ...  
```
### patch
```cpp
#if !BUILDFLAG(IS_IOS)
  auto pref_provider_ptr = std::make_unique<content_settings::BravePrefProvider>(
      prefs_, is_off_the_record_, store_last_modified_, restore_session);
  pref_provider_ = pref_provider_ptr.get();
  content_settings_providers_[ProviderType::kPrefProvider] =
      std::move(pref_provider_ptr);
  user_modifiable_providers_.push_back(pref_provider_.get());
  pref_provider_->AddObserver(this);
#endif


```

### match
```cpp
...
 
 void HostContentSettingsMap::RegisterProfilePrefs(
    user_prefs::PrefRegistrySyncable* registry) { ... 
content_settings::PolicyProvider::RegisterProfilePrefs(registry);
 } 
 >>> 
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_IOS)
void HostContentSettingsMap::RegisterProfilePrefs(
    user_prefs::PrefRegistrySyncable* registry) {
  // Ensure the content settings and PermissionSettings are all registered.
  content_settings::ContentSettingsRegistry::GetInstance();
  content_settings::PermissionSettingsRegistry::GetInstance();

  // Register the prefs for the content settings providers.
  content_settings::DefaultProvider::RegisterProfilePrefs(registry);
  content_settings::BravePrefProvider::RegisterProfilePrefs(registry);
  content_settings::PolicyProvider::RegisterProfilePrefs(registry);
}
#endif


```

