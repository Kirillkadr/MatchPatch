### match
```cpp
...
using media_audio_pulse::StubPathMap;
 #endif 
 // defined(DLOPEN_PULSEAUDIO) 
 >>> 
namespace media {
...
}
 ... 
```
### patch
```cpp
constexpr char kBrowserDisplayName[] = "brave-browser";

```

### match
```cpp
...
 
 namespace pulse { ... 
 
 namespace { ... 
 
 #if BUILDFLAG(GOOGLE_CHROME_BRANDING ) ... 
constexpr char kBrowserDisplayName[] = "google-chrome";  >>> 
 #define PRODUCT_STRING "Google Chrome"
  <<< 
#else
constexpr char kBrowserDisplayName[] = "chromium-browser";
#define PRODUCT_STRING "Chromium"

 ... } ...  } ...  
```
### patch
```cpp
#define PRODUCT_STRING "Brave"

```

### match
```cpp
...
 
 namespace pulse { ... 
 
 namespace { ... 
 
 # else ... 
constexpr char kBrowserDisplayName[] = "chromium-browser";  >>> 
 #define PRODUCT_STRING "Chromium"
  <<<  ...} ...  } ...  
```
### patch
```cpp
#define PRODUCT_STRING "Brave"

```

