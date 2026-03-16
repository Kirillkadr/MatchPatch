### match
```
...
// found in the LICENSE file.
 #include "chrome/app/android/chrome_main_delegate_android.h"
 
 >>> 
#include <memory>

 ... 
```
### patch
```
#include "brave/chromium_src/chrome/app/android/chrome_main_delegate_android.h"

#include "brave/app/brave_main_delegate.h"

```

### match
```
...
 std::optional<int> ChromeMainDelegateAndroid::BasicStartupComplete() { ... 
SetChromeSpecificCommandLineFlags();  >>> 
 return ChromeMainDelegate::BasicStartupComplete();  <<< ... } ...  
```
### patch
```
  return BraveMainDelegate::BasicStartupComplete();

```

### match
```
...
 void ChromeMainDelegateAndroid::PreSandboxStartup() { ...   >>> 
 ChromeMainDelegate::PreSandboxStartup();  <<< ... 
// PoissonAllocationSampler's TLS slots need to be set up before
 ... } ...  
```
### patch
```
  BraveMainDelegate::PreSandboxStartup();

```

