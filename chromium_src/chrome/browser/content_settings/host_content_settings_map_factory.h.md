### match
```
...
 
 # ifndef ... 
#include "base/no_destructor.h"

 #include "chrome/browser/profiles/refcounted_profile_keyed_service_factory.h"
 
 >>> 
class HostContentSettingsMap
 ... 
```
### patch
```
#include "components/keyed_service/content/refcounted_browser_context_keyed_service_factory.h"
#include "components/keyed_service/core/refcounted_keyed_service_factory.h"

```

### match
```
...
 
 # ifndef ... 
// RefcountedBrowserContextKeyedServiceFactory methods:  >>> 
 scoped_refptr<RefcountedKeyedService> BuildServiceInstanceFor(
      content::BrowserContext* context) const override;  <<<  ...
```
### patch
```
  scoped_refptr<RefcountedKeyedService> BuildServiceInstanceFor_ChromiumImpl( content::BrowserContext* context) const; 
  scoped_refptr<RefcountedKeyedService> BuildServiceInstanceFor( content::BrowserContext* context) const override;

```

