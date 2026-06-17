### match
```cpp
...
// found in the LICENSE file.
 #include "components/translate/core/common/translate_util.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/feature_override.h"
#include "brave/components/translate/core/common/brave_translate_constants.h"

```

### match
```cpp
...
 
 namespace translate { ... 
>>> 
 GURL 
 GetTranslateSecurityOrigin() 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
GURL GetTranslateSecurityOrigin_Chromium() {

```

### match
```cpp
...
 
 namespace translate { ... 
>>> 
 bool 
 IsTFLiteLanguageDetectionEnabled() 
 { 
<<< 
// The feature is explicitly disabled on WebView.
 ... } ...  } ...  
```
### patch
```cpp
bool IsTFLiteLanguageDetectionEnabled_Chromium() {

```

### match
```cpp
...
 
 namespace translate { ... 
 
 int GetMaximumNumberOfAutoNever() { ... 
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// Redirect native translate requests to the translate.brave.com (expect the
// script request).
GURL GetTranslateSecurityOrigin() {
  std::string security_origin(kBraveTranslateOrigin);
  base::CommandLine* command_line = base::CommandLine::ForCurrentProcess();
  if (command_line->HasSwitch(switches::kTranslateSecurityOrigin)) {
    security_origin =
        command_line->GetSwitchValueASCII(switches::kTranslateSecurityOrigin);
  }
  return GURL(security_origin);
}
bool IsTFLiteLanguageDetectionEnabled() {
  // This feature is always disabled in Brave.
  return false;
}

```

