### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/live_caption/caption_util.h"

 ... 
```
### patch
```cpp
#include "components/live_caption/caption_util.h"

```

### match
```cpp
...
 
 namespace captions { ...   >>> 
 bool 
 IsLiveCaptionFeatureSupported() 
 {  <<< 
#if !BUILDFLAG(IS_FUCHSIA) && !BUILDFLAG(IS_ANDROID)
  return speech::IsOnDeviceSpeechRecognitionSupported();
#else
  return false;
#endif
 ... } ...  } ...  
```
### patch
```cpp
bool IsLiveCaptionFeatureSupported_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace captions { ... 
 
 std::string GetCaptionSettingsUrl() { ... 
#if BUILDFLAG(IS_CHROMEOS)
  return "chrome://os-settings/audioAndCaptions";
#elif BUILDFLAG(IS_LINUX)
  return "chrome://settings/captions";
#elif BUILDFLAG(IS_WIN)
  return base::win::GetVersion() >= base::win::Version::WIN10
             ? "chrome://settings/accessibility"
             : "chrome://settings/captions";
#elif BUILDFLAG(IS_MAC)
  return "chrome://settings/accessibility";
#else
  NOTREACHED();
#endif
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool IsLiveCaptionFeatureSupported() {
  return false;
}

```

