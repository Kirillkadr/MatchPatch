### match
```cpp
...
 #define CHROME_BROWSER_UI_VIEWS_FRAME_HORIZONTAL_TAB_STRIP_REGION_VIEW_H_
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/gtest_prod_util.h"

```

### match
```cpp
...
 
 class HorizontalTabStripRegionView final : public TabStripRegionView { ... 
// horizontal tab strip. Returns false if the point hits an interactive child
 // view. |point| is in the local coordinate space of |this|. 
 >>> 
 ... } ...  
```
### patch
```cpp
    return false;
  }
  views::Button* new_tab_button() {
    return new_tab_button_;
  }
  friend class BraveVerticalTabStripRegionView;
  friend class BraveTabStrip;
  friend class BraveHorizontalTabStripRegionView;
  FRIEND_TEST_ALL_PREFIXES(VerticalTabStripBrowserTest, MinHeight);

```

### match
```cpp
...
// `render_tab_search_before_tab_strip_` is true.
>>> 
 void UpdateTabStripMargin(); 
<<< 
// Gets called on `Layout` and adjusts the x-axis position of the `view` based
 ... 
```
### patch
```cpp
  virtual void UpdateTabStripMargin();

```

