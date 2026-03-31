### match
```cpp
...
 
 # ifndef ... 
#include "ios/chrome/browser/flags/ios_chrome_field_trials.h"

 #include "ios/web/public/init/web_main_parts.h"
 
 >>> 
namespace display {
class ScopedNativeScreen;
}
 ... 
```
### patch
```cpp
#include "ios/web/public/init/web_main_parts.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 class IOSChromeMainParts : public web::WebMainParts { ... 
 // web::WebMainParts implementation. 
 >>> 
void PreCreateMainMessageLoop() override;
 ... } ...  
```
### patch
```cpp
  void PreCreateMainMessageLoop_ChromiumImpl();

 protected:                                

```

