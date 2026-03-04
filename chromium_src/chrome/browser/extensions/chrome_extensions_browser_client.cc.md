### match
```
...
#include "base/values.h"

 #include "base/version.h"
 
 >>> 
#include "build/build_config.h"

 ...
```
### patch
```
#include "brave/browser/extensions/api/brave_extensions_api_client.h"
#include "brave/browser/extensions/updater/brave_update_client_config.h"

```

### match
```
...
 
 namespace extensions { ... 
 ChromeExtensionsBrowserClient::ChromeExtensionsBrowserClient () ...   >>> 
 api_client_(std::make_unique<ChromeExtensionsAPIClient>()) 
 ,  <<< 
event_router_forwarder_(base::MakeRefCounted<EventRouterForwarder>())
 ... ) ...  } ...
```
### patch
```
      api_client_(std::make_unique<BraveExtensionsAPIClient>()),

```

### match
```
...
 
 namespace extensions { ... 
 
 scoped_refptr<update_client::Configurator>
ChromeExtensionsBrowserClient::CreateUpdateClientConfigurator(
    content::BrowserContext* context) { ... 
if (update_url != extension_urls::GetDefaultWebstoreUpdateUrl()) {
    if (update_url.GetPath() == kCrxUrlPath) {
      override_url = update_url.GetWithEmptyPath().Resolve(kJsonUrlPath);
    } else {
      override_url = update_url;
    }
  }  >>> 
 return ChromeUpdateClientConfig::Create(context, override_url);  <<<  ...} ...  } ...  
```
### patch
```
  return BraveUpdateClientConfig::Create(context, override_url);

```

