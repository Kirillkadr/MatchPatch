### match
```cpp
...
#include "base/feature_list.h"

 #include "base/strings/string_number_conversions.h"
 
 >>> 
#include "chrome/browser/ui/color/chrome_color_id.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/color/brave_color_mixer.h"

```

### match
```cpp
...
>>>
 void 
 AddOmniboxColorMixer 
 ( 
 ui::ColorProvider* provider 
 ,  <<< 
const ui::ColorProviderKey& key
 ... ) ...  
```
### patch
```cpp
void AddOmniboxColorMixer_ChromiumImpl(ui::ColorProvider* provider,

```

### match
```cpp
...
 
 void AddOmniboxColorMixer_ChromiumImpl(ui::ColorProvider* provider,
const ui::ColorProviderKey& key) { ... 
ApplyComposeboxBaselineColors(mixer, key);
 } 
 >>> 
 ... 
```
### patch
```cpp

void AddOmniboxColorMixer(ui::ColorProvider* provider,
                          const ui::ColorProviderKey& key) {
  AddOmniboxColorMixer_ChromiumImpl(provider, key);

#if !BUILDFLAG(IS_ANDROID)
  AddBraveOmniboxColorMixer(provider, key);
#endif  // #if !BUILDFLAG(IS_ANDROID)
}
```

