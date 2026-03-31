### match
```cpp
...
 
 # ifndef ... 
#include "base/no_destructor.h"

 #include "chrome/browser/profiles/profile_keyed_service_factory.h"
 
 >>> 
class GAIAInfoUpdateService
 ... 
```
### patch
```cpp
#include "components/keyed_service/content/browser_context_keyed_service_factory.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 class GAIAInfoUpdateServiceFactory : public ProfileKeyedServiceFactory { ... 
~GAIAInfoUpdateServiceFactory() override;
 // BrowserContextKeyedServiceFactory: 
 >>> 
std::unique_ptr<KeyedService> BuildServiceInstanceForBrowserContext(
      content::BrowserContext* context) const override;
 ... } ...  
```
### patch
```cpp
  std::unique_ptr<KeyedService> BuildServiceInstanceForBrowserContext_ChromiumImpl(
      content::BrowserContext* context) const;

```

