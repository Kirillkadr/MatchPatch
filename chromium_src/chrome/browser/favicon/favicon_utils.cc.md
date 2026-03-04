### match
```
...
#include "chrome/browser/favicon/favicon_utils.h"

 #include "base/hash/sha1.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/components/constants/webui_url_constants.h"

```

### match
```
...
#include "content/public/browser/navigation_controller.h"

 #include "content/public/browser/navigation_entry.h"
 
 >>> 
#include "ui/base/l10n/l10n_util.h"

 ... 
```
### patch
```
#include "content/public/common/url_constants.h"

```

### match
```
...
 
 namespace favicon { ...   >>> 
 bool 
 ShouldThemifyFaviconForEntry(content::NavigationEntry* entry) 
 {  <<< 
const GURL& virtual_url = entry->GetVirtualURL();
 ... } ...  } ...  
```
### patch
```
bool ShouldThemifyFaviconForEntry_ChromiumImpl(content::NavigationEntry* entry) {

```

### match
```
...
 
 namespace favicon { ... 
 
 gfx::ImageSkia ThemeMonochromeFavicon(const gfx::ImageSkia& source,
                                      SkColor background) { ... 
return (color_utils::GetContrastRatio(gfx::kGoogleGrey900, background) >
          color_utils::GetContrastRatio(SK_ColorWHITE, background))
             ? gfx::ImageSkiaOperations::CreateColorMask(source,
                                                         gfx::kGoogleGrey900)
             : gfx::ImageSkiaOperations::CreateColorMask(source, SK_ColorWHITE);
 } 
 >>> 
 ... } ...  
```
### patch
```
bool ShouldThemifyFaviconForEntry(content::NavigationEntry* entry) {
  const GURL& virtual_url = entry->GetVirtualURL();
  // Don't theme for certain brave favicons which are full color
  if (virtual_url.SchemeIs(content::kChromeUIScheme) &&
      (virtual_url.host() == kRewardsPageHost ||
       virtual_url.host() == kWalletPageHost ||
       virtual_url.host() == kAIChatUIHost ||
       virtual_url.host() == chrome::kChromeUINewTabHost)) {
    return false;
  }
  return ShouldThemifyFaviconForEntry_ChromiumImpl(entry);
}


```

