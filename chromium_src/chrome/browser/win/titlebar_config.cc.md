### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/win/titlebar_config.h"
 
 >>> 
#include "chrome/browser/themes/theme_service.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 bool ShouldBrowserCustomDrawTitlebar(BrowserView* browser_view) { ... 
return !ShouldDefaultThemeUseMicaTitlebar() ||
         !ThemeServiceFactory::GetForProfile(browser_view->GetProfile())
              ->UsingSystemTheme() ||
         (!browser_view->browser()->is_type_normal() &&
          !browser_view->browser()->is_type_popup() &&
          !browser_view->browser()->is_type_devtools());
 } 
 >>> 
 ... 
```
### patch
```cpp

OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kWindows11MicaTitlebar, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

