### match
```cpp
...
 #include "base/task/thread_pool.h"
 
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
 
 BrowserRootView::DropTarget* BrowserRootView::GetDropTarget(
    const ui::DropTargetEvent& event) { ... 
>>> 
 ConvertPointToTarget(this, browser_view_->tab_strip_view(), &loc_in_tabstrip); 
<<< 
...} ...  
```
### patch
```cpp
  if (views::View* target_v = browser_view_->tab_strip_view();                                
      tabs::utils::ShouldShowBraveVerticalTabs(browser_view_->browser()) &&
      (target_v == browser_view_->tab_strip_view() ||
       !this->Contains(target_v))) {
    ConvertPointToScreen(this, &loc_in_tabstrip);
    ConvertPointFromScreen(target_v, &loc_in_tabstrip);
  } else {
    ConvertPointToTarget(this, target_v, &loc_in_tabstrip);
  }

```

