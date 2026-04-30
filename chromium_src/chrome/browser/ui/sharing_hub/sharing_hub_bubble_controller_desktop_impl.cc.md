### match
```cpp
...
#include "chrome/browser/ui/sharing_hub/sharing_hub_bubble_view.h"

 #include "chrome/browser/ui/sharing_hub/sharing_hub_window_controller.h"
 
 >>> 
#include "chrome/grit/generated_resources.h"

 ... 
```
### patch
```cpp
#include "chrome/common/pref_names.h"

```

### match
```cpp
...
#include "components/media_router/browser/media_router_dialog_controller.h"

 #include "components/media_router/browser/media_router_metrics.h"
 
 >>> 
#include "content/public/browser/site_instance.h"

 ... 
```
### patch
```cpp
#include "components/prefs/pref_service.h"

```

### match
```cpp
...
 
 namespace sharing_hub { ...   >>> 
 bool 
 SharingHubBubbleControllerDesktopImpl::ShouldOfferOmniboxIcon() 
 {  <<< 
return SharingHubOmniboxEnabled(GetWebContents().GetBrowserContext());
 ... } ...  } ...  
```
### patch
```cpp
bool SharingHubBubbleControllerDesktopImpl::ShouldOfferOmniboxIcon_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace sharing_hub { ... 
SharingHubBubbleControllerDesktopImpl::SharingHubBubbleControllerDesktopImpl(
    content::WebContents* web_contents)
    : content::WebContentsObserver(web_contents),
      content::WebContentsUserData<SharingHubBubbleControllerDesktopImpl>(
          *web_contents) {}
 WEB_CONTENTS_USER_DATA_KEY_IMPL(SharingHubBubbleControllerDesktopImpl); 
 >>> 
 ... } ...  
```
### patch
```cpp
bool SharingHubBubbleControllerDesktopImpl::ShouldOfferOmniboxIcon() {
  const GURL url = GetWebContents().GetLastCommittedURL();

  // To disable share icons in internal pages.
  if (url.is_valid() && !url.SchemeIsHTTPOrHTTPS()) {
    return false;
  }

  // Checks if the kPinShareMenuButton pref is true.
  if (!GetProfile()->GetPrefs()->GetBoolean(prefs::kPinShareMenuButton)) {
    return false;
  }

  return ShouldOfferOmniboxIcon_ChromiumImpl();
}


```

