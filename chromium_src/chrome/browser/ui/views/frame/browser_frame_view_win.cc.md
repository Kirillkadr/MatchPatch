### match
```cpp
...
 #include "base/trace_event/trace_event.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/tabs/vertical_tab_utils.h"

```

### match
```cpp
...
 #include "chrome/browser/themes/theme_properties.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/browser.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/frame/tab_strip_region_view.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/frame/webui_tab_strip_container_view.h"

```

### match
```cpp
...
 
 BrowserFrameViewWin::BrowserFrameViewWin(BrowserWidget* widget,
                                         BrowserView* browser_view)
    : BrowserFrameView(widget, browser_view),
      caption_button_metrics_(std::make_unique<CaptionButtonMetrics>(*this)) { ... 
>>> 
 browser->SupportsWindowFeature(Browser::WindowFeature::kFeatureTitleBar) 
 ; 
<<< 
...} ...  
```
### patch
```cpp
      browser->upportsWindowFeature(Browser::WindowFeature::kFeatureTitleBar) ||
      (Browser::WindowFeature::kFeatureTitleBar == Browser::WindowFeature::kFeatureTitleBar &&
       tabs::utils::SupportsBraveVerticalTabs(browser));

```

