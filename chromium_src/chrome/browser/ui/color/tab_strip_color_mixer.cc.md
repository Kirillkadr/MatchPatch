### match
```cpp
...
>>>
 void 
 AddTabStripColorMixer 
 ( 
 ui::ColorProvider* provider 
 ,  <<< 
const ui::ColorProviderKey& key
 ... ) ...  
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)
#include "brave/browser/ui/color/brave_color_mixer.h"
#include "brave/browser/ui/tabs/brave_tab_color_mixer.h"
#endif

void AddTabStripColorMixer_ChromiumImpl(ui::ColorProvider* provider,

```

### match
```cpp
...
 
 void AddTabStripColorMixer_ChromiumImpl(ui::ColorProvider* provider,
const ui::ColorProviderKey& key) { ... 
mixer[kColorWebUiTabStripTabWaitingSpinning] = {kColorTabThrobberPreconnect};
 } 
 >>> 
 ... 
```
### patch
```cpp

namespace {

void AddBraveTabStripColorMixer(ui::ColorProvider* provider,
                                const ui::ColorProviderKey& key) {
#if !BUILDFLAG(IS_ANDROID)
  AddBravifiedTabStripColorMixer(provider, key);
#endif  // #if !BUILDFLAG(IS_ANDROID)
}

}  // namespace

void AddTabStripColorMixer(ui::ColorProvider* provider,
                           const ui::ColorProviderKey& key) {
  AddTabStripColorMixer_ChromiumImpl(provider, key);
  AddBraveTabStripColorMixer(provider, key);

#if !BUILDFLAG(IS_ANDROID)
  // Set vertical tab mixer after adding tab strip mixer because
  // vertical tab mixer uses tab strip mixer's color.
  tabs::AddBraveTabThemeColorMixer(provider, key);
#endif
}

```

