### match
```cpp
...
#include "base/logging.h"

 #include "base/strings/string_number_conversions.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/color/brave_color_mixer.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 void ApplyGM3OmniboxBackgroundColor(ui::ColorMixer& mixer,
                                    const ui::ColorProviderKey& key) { ... 
if (!key.custom_theme) {
    mixer[kColorLocationBarBackground] = {ui::kColorSysOmniboxContainer};
    mixer[kColorLocationBarBackgroundHovered] =
        ui::GetResultingPaintColor(ui::kColorSysStateHoverBrightBlendProtection,
                                   kColorLocationBarBackground);

    // Update colors to account for "mismatched input/URL" in the omnibox.
    mixer[kColorLocationBarBorderOnMismatch] = {ui::kColorSysNeutralOutline};
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void AddBraveColorMixer(ui::ColorProvider* provider,
                        const ui::ColorProviderKey& key) {
#if !BUILDFLAG(IS_ANDROID)
  AddBraveThemeColorMixer(provider, key);
  AddBravifiedChromeThemeColorMixer(provider, key);
#endif  // #if !BUILDFLAG(IS_ANDROID)
}


```

### match
```cpp
...
>>>
 void 
 AddChromeColorMixer 
 ( 
 ui::ColorProvider* provider 
 ,  <<< 
const ui::ColorProviderKey& key
 ... ) ...  
```
### patch
```cpp
void AddChromeColorMixer_ChromiumImpl(ui::ColorProvider* provider,

```

### match
```cpp
...
 
 void AddChromeColorMixer_ChromiumImpl(ui::ColorProvider* provider,
const ui::ColorProviderKey& key) { ... 
mixer[ui::kColorFrameInactive] = {SK_ColorGRAY};
 } 
 >>> 
 ... 
```
### patch
```cpp

void AddChromeColorMixer(ui::ColorProvider* provider,
                         const ui::ColorProviderKey& key) {
  AddChromeColorMixer_ChromiumImpl(provider, key);
  AddBraveColorMixer(provider, key);
}

```

