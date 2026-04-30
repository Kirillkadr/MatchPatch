### match
```cpp
...
#include "chrome/browser/ui/color/chrome_color_id.h"

 #include "chrome/browser/ui/color/chrome_color_provider_utils.h"
 
 >>> 
#include "ui/color/color_id.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/color/brave_material_side_panel_color_mixer.h"

```

### match
```cpp
...
>>>
 void 
 AddMaterialSidePanelColorMixer 
 ( 
 ui::ColorProvider* provider 
 ,  <<< 
const ui::ColorProviderKey& key
 ... ) ...  
```
### patch
```cpp
void AddMaterialSidePanelColorMixer_ChromiumImpl(ui::ColorProvider* provider,

```

### match
```cpp
...
 
 void AddMaterialSidePanelColorMixer_ChromiumImpl(ui::ColorProvider* provider,
const ui::ColorProviderKey& key) { ... 
mixer[kColorSidePanelResizeAreaHandle] = {ui::kColorSysOnSurfaceSubtle};
 } 
 >>> 
 ... 
```
### patch
```cpp

void AddMaterialSidePanelColorMixer(ui::ColorProvider* provider,
                                    const ui::ColorProviderKey& key) {
  AddMaterialSidePanelColorMixer_ChromiumImpl(provider, key);
#if !BUILDFLAG(IS_ANDROID)
  AddBraveMaterialSidePanelColorMixer(provider, key);
#endif
}
```

