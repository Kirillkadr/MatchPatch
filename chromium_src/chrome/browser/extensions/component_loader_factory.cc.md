### match
```
...
#include "base/memory/ptr_util.h"

 #include "base/no_destructor.h"
 
 >>> 
#include "chrome/browser/extensions/component_loader.h"

 ... 
```
### patch
```
#include "brave/browser/extensions/brave_component_loader.h"

```

### match
```
...
 
 namespace extensions { ... 
 
 std::unique_ptr<KeyedService>
ComponentLoaderFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const { ... 
// Use `new` to access private constructor.  >>> 
 return base::WrapUnique(new ComponentLoader(profile));  <<<  ...} ...  } ...  
```
### patch
```
  return base::WrapUnique(new BraveComponentLoader(profile));

```

