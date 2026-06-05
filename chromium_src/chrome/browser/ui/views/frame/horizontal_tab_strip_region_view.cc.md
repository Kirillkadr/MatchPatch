### match
```cpp
...
 #include "base/task/single_thread_task_runner.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/tabs/brave_browser_tab_strip_controller.h"
#include "brave/browser/ui/views/tabs/brave_new_tab_button.h"
#include "brave/browser/ui/views/tabs/brave_tab_strip.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/frame/browser_view.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/frame/tab_strip_region_view.h"

```

### match
```cpp
...
>>>
 auto 
 tabstrip_controller 
 = 
 std::make_unique<BrowserTabStripController> 
 ( 
<<< 
...) ...  
```
### patch
```cpp
  auto tabstrip_controller = std::make_unique<BraveBrowserTabStripController>(

```

### match
```cpp
...
>>>
 auto 
 tab_strip 
 = 
 std::make_unique<TabStrip> 
 ( 
 std::move(tabstrip_controller) 
 , 
<<< 
...) ...  
```
### patch
```cpp
  auto tab_strip = std::make_unique<BraveTabStrip>(std::move(tabstrip_controller),

```

### match
```cpp
...
 
 HorizontalTabStripRegionView::HorizontalTabStripRegionView(
    BrowserView* browser_view)
    : profile_(browser_view->GetProfile()),
      render_tab_search_before_tab_strip_(
          !tabs::GetDefaultTabSearchRightAligned() ||
          base::FeatureList::IsEnabled(tabs::kHorizontalTabStripComboButton)),
      tab_search_position_metrics_logger_(
          std::make_unique<TabSearchPositionMetricsLogger>(
              browser_view->browser())),
      action_view_controller_(std::make_unique<views::ActionViewController>()) { ... 
 
 if (ShouldShowNewTabButton(browser)) { ... 
>>> 
 std::make_unique<NewTabButton> 
 ( 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
        std::make_unique<BraveNewTabButton>(

```

### match
```cpp
...
 
 void HorizontalTabStripRegionView::InitializeTabStrip() { ... 
>>> 
 static_cast<BrowserTabStripController*>(tab_strip_->controller()) 
<<< 
...} ...  
```
### patch
```cpp
  static_cast<BraveBrowserTabStripController*>(tab_strip_->controller())

```

### match
```cpp
...
 
 void HorizontalTabStripRegionView::ResetTabStrip() { ... 
>>> 
 static_cast<BrowserTabStripController*>(tab_strip_->controller())->Reset(); 
<<< 
...} ...  
```
### patch
```cpp
  static_cast<BraveBrowserTabStripController*>(tab_strip_->controller())->Reset();

```

### match
```cpp
...
 
 void HorizontalTabStripRegionView::UpdateButtonBorders() { ... 
>>> 
 NewTabButton::kButtonSize.height() 
 ; 
<<< 
...} ...  
```
### patch
```cpp
      BraveNewTabButton::GetButtonSize().height();

```

