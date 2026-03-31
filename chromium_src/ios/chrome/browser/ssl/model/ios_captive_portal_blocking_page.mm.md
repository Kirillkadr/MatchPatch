### match
```cpp
...
#import "ios/chrome/browser/ssl/model/captive_portal_tab_helper.h"

 #import "ui/base/l10n/l10n_util.h"
 
 >>> 
IOSCaptivePortalBlockingPage::IOSCaptivePortalBlockingPage(
    web::WebState* web_state,
    const GURL& request_url,
    const GURL& landing_url,
    security_interstitials::IOSBlockingPageControllerClient* client)
    : security_interstitials::IOSSecurityInterstitialPage(web_state,
                                                          request_url,
                                                          client),
      landing_url_(landing_url) {
  captive_portal::CaptivePortalMetrics::LogCaptivePortalBlockingPageEvent(
      captive_portal::CaptivePortalMetrics::SHOW_ALL);
}
 ... 
```
### patch
```cpp
#include "base/check.h"
#include "base/memory/raw_ptr.h"
#include "ios/chrome/browser/ssl/model/captive_portal_tab_helper.h"
#include "ios/chrome/browser/web/model/web_navigation_util.h"
#include "ios/web/public/lazy_web_state_user_data.h"
#include "ios/web/public/navigation/navigation_manager.h"
#include "ios/web/public/web_state.h"
#include "ios/web/public/web_state_observer.h"

// A custom captive portal tab helper that instead just loads the landing URL
// directly into the current WebState instead of attempting to open it in a new
// tab since we dont use WebStateList & its insertion agent on iOS
class BraveCaptivePortalTabHelper
    : public web::LazyWebStateUserData<BraveCaptivePortalTabHelper>,
      web::WebStateObserver {
 public:
  BraveCaptivePortalTabHelper(const BraveCaptivePortalTabHelper&) = delete;
  BraveCaptivePortalTabHelper& operator=(const BraveCaptivePortalTabHelper&) =
      delete;

  ~BraveCaptivePortalTabHelper() override {
    if (web_state_) {
      web_state_->RemoveObserver(this);
    }
  }

  // Displays the Captive Portal Login page at `landing_url`.
  void DisplayCaptivePortalLoginPage(GURL landing_url) {
    if (!web_state_) {
      return;
    }
    web_state_->GetNavigationManager()->LoadURLWithParams(
        web_navigation_util::CreateWebLoadParams(
            landing_url, ui::PAGE_TRANSITION_TYPED, nullptr));
  }

  // WebObserver
  void WebStateDestroyed(web::WebState* web_state) override {
    DCHECK_EQ(web_state_, web_state);
    web_state_->RemoveObserver(this);
    web_state_ = nullptr;
  }

 private:
  friend class web::LazyWebStateUserData<BraveCaptivePortalTabHelper>;
  BraveCaptivePortalTabHelper(web::WebState* web_state)
      : web_state_(web_state) {
    web_state_->AddObserver(this);
  }
  raw_ptr<web::WebState> web_state_ = nullptr;
};

```

### match
```cpp
...
 
 void IOSCaptivePortalBlockingPage::HandleCommand(
    security_interstitials::SecurityInterstitialCommand command) { ... 
 
 if (command == security_interstitials::CMD_OPEN_LOGIN) { ...   >>> 
 CaptivePortalTabHelper::FromWebState(web_state())  <<<  ...} ...  } ...  
```
### patch
```cpp
    BraveCaptivePortalTabHelper::FromWebState(web_state())

```

