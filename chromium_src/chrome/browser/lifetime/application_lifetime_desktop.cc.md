### match
```
...
#include "base/time/time.h"

 #include "base/types/strong_alias.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/browser/sparkle_buildflags.h"

```

### match
```
...
#include "content/public/browser/browser_task_traits.h"

 #include "content/public/browser/browser_thread.h"
 
 >>> 
#if BUILDFLAG(IS_CHROMEOS)
#include "chrome/browser/ash/boot_times_recorder/boot_times_recorder.h"
#include "chrome/browser/lifetime/application_lifetime_chromeos.h"
#include "chromeos/ash/components/login/session/session_termination_manager.h"
#else  // !BUILDFLAG(IS_CHROMEOS)
#include "chrome/browser/ui/profiles/profile_picker.h"
#endif
 ... 
```
### patch
```
#if BUILDFLAG(ENABLE_SPARKLE)

#include "brave/browser/ui/webui/settings/brave_relaunch_handler_mac.h"

#define AttemptRestart AttemptRestart_ChromiumImpl
#define RelaunchIgnoreUnloadHandlers RelaunchIgnoreUnloadHandlers_ChromiumImpl

#include <chrome/browser/lifetime/application_lifetime_desktop.cc>

#undef RelaunchIgnoreUnloadHandlers
#undef AttemptRestart

namespace chrome {

void AttemptRestart() {
  if (!brave_relaunch_handler::RelaunchOnMac()) {
    AttemptRestart_ChromiumImpl();
  }
}

void RelaunchIgnoreUnloadHandlers() {
  if (!brave_relaunch_handler::RelaunchOnMac()) {
    RelaunchIgnoreUnloadHandlers_ChromiumImpl();
  }
}

}  // namespace chrome

#else


```

### match
```
...
 
 #if BUILDFLAG(ENABLE_SPARKLE ) ... 
 
 # else ... 
 
 namespace chrome { ... 
bool AreAllBrowsersCloseable() {
  if (GlobalBrowserCollection::GetInstance()->IsEmpty()) {
    return true;
  }

  // If there are any downloads active, all browsers are not closeable.
  // However, this does not block for malicious downloads.
  if (DownloadCoreService::BlockingShutdownCountAllProfiles() > 0) {
    return false;
  }

  // Check TabsNeedBeforeUnloadFired().
  bool all_closeable = true;
  ForEachCurrentBrowserWindowInterfaceOrderedByActivation(
      [&all_closeable](BrowserWindowInterface* bwi) {
        if (bwi->GetBrowserForMigrationOnly()->TabsNeedBeforeUnloadFired()) {
          all_closeable = false;
        }
        return all_closeable;
      });
  return all_closeable;
}
 } 
 // namespace chrome 
 >>> 
 ... 
```
### patch
```
#endif  // BUILDFLAG(ENABLE_SPARKLE)

```

