### match
```
...
#include "chrome/browser/search_engines/template_url_service_factory.h"

 #include "chrome/browser/supervised_user/family_link_settings_service_factory.h"
 
 >>> 
#include "chrome/common/buildflags.h"

 ...
```
### patch
```
#include "chrome/browser/supervised_user/supervised_user_settings_service_factory.h"

```

### match
```
...
#include "components/content_settings/core/browser/content_settings_pref_provider.h"

 #include "components/content_settings/core/browser/host_content_settings_map.h"
 
 >>> 
#include "components/permissions/features.h"

 ...
```
### patch
```
#include "components/keyed_service/content/browser_context_keyed_service_factory.h"
#include "components/keyed_service/core/simple_keyed_service_factory.h"

```

### match
```
...
 #if BUILDFLAG(ENABLE_EXTENSIONS ) ... 
#include "extensions/browser/api/content_settings/content_settings_custom_extension_provider.h"  // nogncheck

 #include "extensions/browser/api/content_settings/content_settings_service.h"  // nogncheck
 
 >>> 
 ...
```
### patch
```
#include "extensions/browser/browser_context_keyed_api_factory.h"


```

### match
```
...
 scoped_refptr<RefcountedKeyedService>
 >>> 
 HostContentSettingsMapFactory::BuildServiceInstanceFor 
 (  <<< 
content::BrowserContext* context ) ...
```
### patch
```
    HostContentSettingsMapFactory::BuildServiceInstanceFor_ChromiumImpl(

```

### match
```
...
 scoped_refptr<RefcountedKeyedService>
        HostContentSettingsMapFactory::BuildServiceInstanceFor_ChromiumImpl(
content::BrowserContext* context) const { ... 
return settings_map;
 } 
 >>> 
 ... 
```
### patch
```

scoped_refptr<RefcountedKeyedService>
HostContentSettingsMapFactory::BuildServiceInstanceFor(
    content::BrowserContext* context) const {
  scoped_refptr<RefcountedKeyedService> settings_map =
      BuildServiceInstanceFor_ChromiumImpl(context);
  auto remote_list_provider_ptr =
      std::make_unique<content_settings::RemoteListProvider>();
  static_cast<HostContentSettingsMap*>(settings_map.get())
      ->RegisterProvider(ProviderType::kRemoteListProvider,
                         std::move(remote_list_provider_ptr));
  return settings_map;
}
```

