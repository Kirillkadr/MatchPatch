### match
```cpp
...
// found in the LICENSE file.
 #include "components/security_interstitials/content/ssl_blocking_page_base.h"
 
 >>> 
#include "components/safe_browsing/core/common/safe_browsing_prefs.h"

 ... 
```
### patch
```cpp
#include "components/safe_browsing/core/common/safe_browsing_prefs.h"

```

### match
```cpp
...
 
 bool SSLBlockingPageBase::ShouldShowEnhancedProtectionMessage() { ... 
 safe_browsing::IsSafeBrowsingPolicyManaged(*pref_service) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
      return false;

```

