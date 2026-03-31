### match
```cpp
...
#include "base/trace_event/trace_event.h"

 #include "base/values.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ...
```
### patch
```cpp
#include "brave/browser/brave_browser_process_impl.h"

```

### match
```cpp
...
#else
#include <vector>

#include "base/no_destructor.h"
#include "chrome/browser/apps/app_service/app_service_proxy_factory.h"
#include "chrome/browser/apps/app_service/publishers/publisher_host_factory_impl.h"
#include "chrome/browser/headless/chrome_browser_main_extra_parts_headless.h"
#include "chrome/browser/lifetime/smart_restart_metrics_observer.h"
#include "chrome/browser/profiles/delete_profile_helper.h"
#include "chrome/browser/resource_coordinator/tab_manager.h"
#include "chrome/browser/ui/uma_browsing_activity_observer.h"
#include "chrome/browser/upgrade_detector/upgrade_detector.h"
#include "chrome/browser/usb/web_usb_detector.h"
#include "chrome/browser/win/browser_util.h"
#include "components/soda/soda_installer.h"
#include "components/soda/soda_util.h"

 #endif 
 >>> 
 ...
```
### patch
```cpp
#if BUILDFLAG(IS_MAC)
#include "brave/browser/brave_browser_main_parts_mac.h"
#undef ChromeBrowserMainPartsMac
#define ChromeBrowserMainPartsMac BraveBrowserMainPartsMac
#endif  // BUILDFLAG(IS_MAC)
#define ChromeBrowserMainParts ChromeBrowserMainParts_ChromiumImpl

```

### match
```cpp
...
   >>> 
 browser_process_ = std::make_unique<BrowserProcessImpl>(startup_data_);  <<< 
...
```
### patch
```cpp
browser_process_ = std::make_unique<BraveBrowserProcessImpl>(startup_data_);

```

### match
```cpp
...
bool ChromeBrowserMainParts::ProcessSingletonNotificationForTesting(
    base::CommandLine command_line) {
  return ProcessSingletonNotificationCallback(command_line,
                                              /*current_directory=*/{});
}
 #endif 
 // BUILDFLAG(ENABLE_PROCESS_SINGLETON) 
 >>> 
 ... 
```
### patch
```cpp

#undef ChromeBrowserMainParts
#if BUILDFLAG(IS_MAC)
#undef ChromeBrowserMainPartsMac
#endif  // BUILDFLAG(IS_MAC)

```

