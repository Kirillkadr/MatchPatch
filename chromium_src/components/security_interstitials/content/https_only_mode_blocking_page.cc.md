### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/security_interstitials/content/https_only_mode_blocking_page.h"

 ... 
```
### patch
```cpp
#include "components/security_interstitials/content/https_only_mode_blocking_page.h"

```

### match
```cpp
...
#include "components/security_interstitials/content/https_only_mode_blocking_page.h"

 #include "components/security_interstitials/content/https_only_mode_blocking_page.h"
 
 >>> 
#include "base/logging.h"

 ... 
```
### patch
```cpp
// Avoid modifying `OpenUrlInNewForegroundTab` definition.
#include "components/security_interstitials/content/security_interstitial_controller_client.h"

```

### match
```cpp
...
 namespace 
 security_interstitials 
 { 
 >>> 
// static
 ... } ...  
```
### patch
```cpp
namespace {
constexpr char kBraveLearnMoreLink[] =
    "https://support.brave.app/hc/en-us/articles/15513090104717";
}  // namespace

```

### match
```cpp
...
 
 namespace security_interstitials { ... 
 
 void HttpsOnlyModeBlockingPage::CommandReceived(const std::string& command) { ... 
 
 case security_interstitials : ... 
controller()->metrics_helper()->RecordUserInteraction(
          security_interstitials::MetricsHelper::SHOW_LEARN_MORE);
>>> 
 controller()->OpenUrlInNewForegroundTab(GURL(kLearnMoreLink)); 
<<< 
break;
 ... } ...  } ...  
```
### patch
```cpp
      controller()->OpenUrlInNewForegroundTab(GURL(kBraveLearnMoreLink));

```

