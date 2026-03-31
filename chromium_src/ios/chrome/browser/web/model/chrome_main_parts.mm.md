### match
```cpp
...
#import "ui/base/resource/resource_bundle.h"

 #import "ui/display/screen.h"
 
 >>> 
#if DCHECK_IS_ON()
#import "ui/display/screen_base.h"
#endif
 ... 
```
### patch
```cpp
#include "ios/chrome/browser/web/model/chrome_main_parts.h"
#include "brave/ios/browser/application_context/brave_application_context_impl.h"

```

### match
```cpp
...
>>>
 void 
 IOSChromeMainParts::PreCreateMainMessageLoop() 
 {  <<< 
#if !BUILDFLAG(USE_BLINK)
  l10n_util::OverrideLocaleWithCocoaLocale();
#endif
 ... } ...  
```
### patch
```cpp
void IOSChromeMainParts::PreCreateMainMessageLoop_ChromiumImpl() {

```

### match
```cpp
...
>>>
 application_context_.reset 
 ( 
 new 
 ApplicationContextImpl 
 (  <<< 
local_state_task_runner.get()
 ... ) ...  ) ...  
```
### patch
```cpp
  application_context_.reset(new BraveApplicationContextImpl(

```

### match
```cpp
...
 
 void IOSChromeMainParts::StartMetricsRecording() { ... 
application_context_->GetMetricsServicesManager()->UpdateUploadPermissions();
 } 
 >>> 
 ... 
```
### patch
```cpp
void IOSChromeMainParts::PreCreateMainMessageLoop() {
  IOSChromeMainParts::PreCreateMainMessageLoop_ChromiumImpl();
}
```

