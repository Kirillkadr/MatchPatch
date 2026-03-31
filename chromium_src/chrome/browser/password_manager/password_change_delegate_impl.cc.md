### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/password_manager/password_change_delegate_impl.h"

 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_CONTAINERS)
#define GetSiteInstanceForNewTab(profile, url) \
  GetSiteInstanceForNewTab(profile, url, std::nullopt)
#endif  // BUILDFLAG(ENABLE_CONTAINERS)

```

### match
```cpp
...
#include "base/time/time.h"

 #include "base/timer/timer.h"
 
 >>> 
#include "chrome/browser/affiliations/affiliation_service_factory.h"

 ... 
```
### patch
```cpp
#include "brave/components/containers/buildflags/buildflags.h"

```

### match
```cpp
...
 
 void PasswordChangeDelegateImpl::ResetInternalState() { ... 
otp_fields_detected_subscription_ = {};
 } 
 >>> 
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_CONTAINERS)
#undef GetSiteInstanceForNewTab
#endif  // BUILDFLAG(ENABLE_CONTAINERS)
```

