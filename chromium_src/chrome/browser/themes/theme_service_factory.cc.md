### match
```cpp
...
#include "base/no_destructor.h"

 #include "base/trace_event/trace_event.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/themes/brave_theme_service.h"

```

### match
```cpp
...
#include "extensions/browser/extension_registry_factory.h"

 #include "ui/base/mojom/themes.mojom.h"
 
 >>> 
#if BUILDFLAG(IS_WIN)
#include "chrome/browser/themes/theme_helper_win.h"
#endif
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_LINUX)
#define BRAVE_THEMESERVICEFACTORY_BUILDSERVICEINSTANCEFOR \
  using ThemeService = BraveThemeService;
#else
// On Linux ThemeServiceAuraLinux derives from BraveThemeService instead.
#define BRAVE_THEMESERVICEFACTORY_BUILDSERVICEINSTANCEFOR
#endif


```

### match
```cpp
...
 
 void ThemeServiceFactory::BrowserContextDestroyed(
    content::BrowserContext* browser_context) { ... 
BrowserContextKeyedServiceFactory::BrowserContextDestroyed(browser_context);
 } 
 >>> 
 ... 
```
### patch
```cpp

#undef BRAVE_THEMESERVICEFACTORY_BUILDSERVICEINSTANCEFOR
```

