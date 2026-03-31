### match
```cpp
...
#include "chrome/browser/privacy_sandbox/privacy_sandbox_settings_factory.h"

 #include "base/no_destructor.h"
 
 >>> 
#include "chrome/browser/content_settings/cookie_settings_factory.h"

 ... 
```
### patch
```cpp
#include "brave/components/privacy_sandbox/brave_privacy_sandbox_settings.h"

```

### match
```cpp
...
 std::unique_ptr<KeyedService>
  >>> 
 PrivacySandboxSettingsFactory::BuildServiceInstanceForBrowserContext 
 (  <<< 
content::BrowserContext* context
 ... ) ...  
```
### patch
```cpp
PrivacySandboxSettingsFactory::BuildServiceInstanceForBrowserContext_ChromiumImpl(

```

### match
```cpp
...
 
 std::unique_ptr<KeyedService>
PrivacySandboxSettingsFactory::BuildServiceInstanceForBrowserContext_ChromiumImpl(
content::BrowserContext* context) const { ... 
return std::make_unique<privacy_sandbox::PrivacySandboxSettingsImpl>(
      std::make_unique<PrivacySandboxSettingsDelegate>(
          profile, GetSingletonPrivacySandboxCountries()),
      HostContentSettingsMapFactory::GetForProfile(profile),
      CookieSettingsFactory::GetForProfile(profile), profile->GetPrefs());
 } 
 >>> 
 ... 
```
### patch
```cpp

std::unique_ptr<KeyedService>
PrivacySandboxSettingsFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const {
  Profile* profile = Profile::FromBrowserContext(context);

  return std::make_unique<BravePrivacySandboxSettings>(
      nullptr /*delegate*/, nullptr /*host_content_settings_map*/,
      nullptr /*cookie_settings*/, profile->GetPrefs());
}
```

