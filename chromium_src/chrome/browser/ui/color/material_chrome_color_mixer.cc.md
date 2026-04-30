### match
```cpp
...
#include "chrome/browser/ui/color/material_chrome_color_mixer.h"

 #include "base/feature_list.h"
 
 >>> 
#include "chrome/browser/ui/color/chrome_color_id.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/color/material_brave_color_mixer.h"

```

### match
```cpp
...
>>>
 void 
 AddMaterialChromeColorMixer 
 ( 
 ui::ColorProvider* provider 
 ,  <<< 
const ui::ColorProviderKey& key
 ... ) ...  
```
### patch
```cpp
void AddMaterialChromeColorMixer_ChromiumImpl(ui::ColorProvider* provider,

```

### match
```cpp
...
 
 void AddMaterialChromeColorMixer_ChromiumImpl(ui::ColorProvider* provider,
const ui::ColorProviderKey& key) { ... 
mixer[kColorGlicSelectionOverlayToastCancelButton] = {
      ui::kColorSysInversePrimary};
 } 
 >>> 
 ... 
```
### patch
```cpp

void AddMaterialChromeColorMixer(ui::ColorProvider* provider,
                                 const ui::ColorProviderKey& key) {
  AddMaterialChromeColorMixer_ChromiumImpl(provider, key);

#if !BUILDFLAG(IS_ANDROID)
  AddMaterialBraveColorMixer(provider, key);
#endif
}
```

