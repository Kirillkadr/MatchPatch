### match
```cpp
...
// found in the LICENSE file.
 #include "components/safe_browsing/content/browser/base_blocking_page.h"
 
 >>> 
#include <cstddef>

 ...
```
### patch
```cpp
#include "components/security_interstitials/core/safe_browsing_loud_error_ui.h"

```

### match
```cpp
...
using security_interstitials::BaseSafeBrowsingErrorUI;
>>> 
 using security_interstitials::SafeBrowsingLoudErrorUI; 
<<< 
using security_interstitials::SecurityInterstitialControllerClient;
 ...
```
### patch
```cpp
using security_interstitials::BraveSafeBrowsingLoudErrorUI;

```

### match
```cpp
...
... 
>>> 
 sb_error_ui_ 
 ( 
 std::make_unique<SafeBrowsingLoudErrorUI> 
 ( 
<<< 
 ...
```
### patch
```cpp
sb_error_ui_(std::make_unique<BraveSafeBrowsingLoudErrorUI>(

```

### match
```cpp
...
 
 namespace safe_browsing { ... 
 
 bool BaseBlockingPage::ShouldReportThreatDetails(SBThreatType threat_type) { ... 
return threat_type == SB_THREAT_TYPE_BILLING ||
         threat_type == SB_THREAT_TYPE_URL_CLIENT_SIDE_PHISHING ||
         threat_type == SB_THREAT_TYPE_URL_MALWARE ||
         threat_type == SB_THREAT_TYPE_URL_PHISHING ||
         threat_type == SB_THREAT_TYPE_URL_UNWANTED;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
constexpr char kSafeBrowsingHelpCenterURL[] =
    "https://support.brave.app/hc/en-us/articles/"
    "15222663599629-Safe-Browsing-in-Brave";

}  // namespace

namespace security_interstitials {

class BraveSafeBrowsingLoudErrorUI : public SafeBrowsingLoudErrorUI {
 public:
  using SafeBrowsingLoudErrorUI::SafeBrowsingLoudErrorUI;

  void HandleCommand(SecurityInterstitialCommand command) override {
    if (command == CMD_OPEN_HELP_CENTER) {
      controller()->OpenURL(should_open_links_in_new_tab(),
                            GURL(kSafeBrowsingHelpCenterURL));
    } else {
      SafeBrowsingLoudErrorUI::HandleCommand(command);
    }
  }
};

}  // namespace security_interstitials

```

