### match
```cpp
...
#include <utility>

 #include "base/base64.h"
 
 >>> 
#include "base/command_line.h"

 ...
```
### patch
```cpp
#include "base/check.h"

```

### match
```cpp
...   >>> 
 bool 
 MediaRouterEnabled(content::BrowserContext* context) 
 {  <<< 
 ...
```
### patch
```cpp
bool MediaRouterEnabled_ChromiumImpl(content::BrowserContext* context) {

```

### match
```cpp
...
bool IsCastMessageLoggingEnabled() {
  return base::FeatureList::IsEnabled(kCastMessageLogging);
}
#endif  // !BUILDFLAG(IS_ANDROID) ||
        // BUILDFLAG(ENABLE_DESKTOP_ANDROID_EXTENSIONS)

 >>> 
 ...
```
### patch
```cpp
bool MediaRouterEnabled(content::BrowserContext* context) {
  if (context->IsTor()) {
    // Disable Media Router in Tor windows.
    return false;
  }
#if BUILDFLAG(IS_ANDROID)
  return MediaRouterEnabled_ChromiumImpl(context);
#else
  if (!base::FeatureList::IsEnabled(kMediaRouter)) {
    return false;
  }
  const PrefService::Preference* pref = GetMediaRouterPref(context);
  CHECK(pref->GetValue()->is_bool());
  // Chromium has a pref for Media Router but it is only controlled via
  // enterprise policy. In Brave, the pref can be controlled both via
  // brave://settings/extensions and enterprise policy, with the latter taking
  // precedence.
  if (pref->IsManaged()) {
    return MediaRouterEnabled_ChromiumImpl(context);
  }
  return pref->GetValue()->GetBool();
#endif
}



```

