### match
```cpp
...
 
 # ifndef ... 
 #define CHROME_BROWSER_THEMES_THEME_SERVICE_AURA_LINUX_H_
 
 >>> 
#include "chrome/browser/themes/theme_service.h"

 ... 
```
### patch
```cpp
#include "brave/browser/themes/brave_theme_service.h"

```

### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 ThemeServiceAuraLinux 
 : public ThemeService 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
class ThemeServiceAuraLinux : public BraveThemeService {

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ThemeServiceAuraLinux : public BraveThemeService { ...   >>> 
 using ThemeService::ThemeService;  <<< 
ThemeServiceAuraLinux(const ThemeServiceAuraLinux&) = delete;
 ... } ...  
```
### patch
```cpp
  using BraveThemeService::BraveThemeService;

```

