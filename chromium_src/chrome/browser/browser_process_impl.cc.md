### match
```cpp
...
#include "ui/base/ui_base_features.h"

 #include "ui/base/unowned_user_data/unowned_user_data_host.h"
 
 >>> 
#if BUILDFLAG(IS_WIN)
#include "base/win/windows_version.h"
#include "chrome/browser/browser_features.h"
#include "chrome/browser/os_crypt/app_bound_encryption_provider_win.h"
#include "chrome/installer/util/install_util.h"
#include "components/app_launch_prefetch/app_launch_prefetch.h"
#include "components/os_crypt/async/browser/dpapi_key_provider.h"
#elif BUILDFLAG(IS_MAC)
#include "chrome/browser/chrome_browser_main_mac.h"
#include "chrome/browser/media/webrtc/system_media_capture_permissions_stats_mac.h"
#endif
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_EXTENSIONS)
#include "brave/browser/extensions/brave_extensions_browser_client_impl.h"
#define ChromeExtensionsBrowserClient BraveExtensionsBrowserClientImpl
#endif


```

### match
```cpp
...
void BrowserProcessImpl::OnPendingRestartResult(
    bool is_update_pending_restart) {
  // Make sure that the browser is still in the background after returning from
  // the check.
  if (is_update_pending_restart && IsRunningInBackground()) {
    DLOG(WARNING) << "Detected update.  Restarting browser.";
    RestartBackgroundInstance();
  }
}
 #endif 
 // BUILDFLAG(IS_WIN) || BUILDFLAG(IS_LINUX) 
 >>> 
 ... 
```
### patch
```cpp

#if BUILDFLAG(ENABLE_EXTENSIONS)
#undef ChromeExtensionsBrowserClient
#endif

```

