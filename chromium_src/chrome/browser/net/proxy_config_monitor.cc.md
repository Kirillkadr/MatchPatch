### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/net/proxy_config_monitor.h"

 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_TOR)
#include "brave/browser/tor/tor_profile_service_factory.h"
#include "brave/components/tor/tor_profile_service.h"
#include "net/proxy_resolution/proxy_config_service.h"
#endif

namespace {

#if BUILDFLAG(ENABLE_TOR)
std::unique_ptr<net::ProxyConfigService> CreateProxyConfigServiceTor(
    Profile* profile) {
  auto* tor_service = TorProfileServiceFactory::GetForContext(profile);
  DCHECK(tor_service);
  return tor_service->CreateProxyConfigService();
}
#endif  // BUILDFLAG(ENABLE_TOR)

}  // namespace

#if BUILDFLAG(ENABLE_TOR)
#define BRAVE_PROXY_CONFIG_MONITOR \
  if (profile && profile->IsTor()) \
    proxy_config_service_ = CreateProxyConfigServiceTor(profile); \
  else
#else
#define BRAVE_PROXY_CONFIG_MONITOR
#endif

```

### match
```cpp
...
#if BUILDFLAG(ENABLE_TOR)
#define BRAVE_PROXY_CONFIG_MONITOR \
  if (profile && profile->IsTor()) \
    proxy_config_service_ = CreateProxyConfigServiceTor(profile); \
  else
#else
#define BRAVE_PROXY_CONFIG_MONITOR
#endif
 #include "chrome/browser/net/proxy_config_monitor.h"
 
 >>> 
#include <utility>

 ... 
```
### patch
```cpp
#include <memory>

```

### match
```cpp
...
#include <memory>

 #include <utility>
 
 >>> 
#include "base/strings/utf_string_conversions.h"

 ... 
```
### patch
```cpp
#include "base/check.h"


```

### match
```cpp
...
#include "base/check.h"

 #include "base/strings/utf_string_conversions.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/tor/buildflags/buildflags.h"

```

### match
```cpp
...
void ProxyConfigMonitor::OnRequestMaybeFailedDueToProxySettings(
    int32_t net_error) {
  DCHECK(BrowserThread::CurrentlyOn(BrowserThread::UI) ||
         !BrowserThread::IsThreadInitialized(BrowserThread::UI));

  if (net_error >= 0) {
    // If the error is obviously wrong, don't dispatch it to extensions. If the
    // PAC executor process is compromised, then |net_error| could be attacker
    // controlled.
    return;
  }

  extensions::ProxyEventRouter::GetInstance()->OnProxyError(profile_,
                                                            net_error);
}
 #endif 
 // BUILDFLAG(ENABLE_EXTENSIONS_CORE) 
 >>> 
 ... 
```
### patch
```cpp
#undef BRAVE_PROXY_CONFIG_MONITOR
```

