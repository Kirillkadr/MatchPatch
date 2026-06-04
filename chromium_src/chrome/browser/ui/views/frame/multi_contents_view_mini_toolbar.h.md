### match
```cpp
...
 #include <optional>
 
 >>> 
 ... 
```
### patch
```cpp
#include <memory>

```

### match
```cpp
...
 #include "chrome/browser/ui/color/chrome_color_id.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/tabs/split_tab_menu_model.h"

```

### match
```cpp
...
 
 namespace views { ... 
 } 
 // namespace views 
 >>> 
// MultiContentsViewMiniToolbar is shown for the inactive side of a split and
 ... 
```
### patch
```cpp
namespace gfx {
struct VectorIcon;
}  // namespace gfx


```

### match
```cpp
...
>>>
 void UpdateState(bool is_active, bool is_highlighted); 
<<< 
// Trigger an update of the tab data used to populate the mini toolbar.
 ... 
```
### patch
```cpp
  virtual void UpdateState(bool is_active, bool is_highlighted);
  static const gfx::VectorIcon& GetMoreVerticalIcon();
  static std::unique_ptr<ui::SimpleMenuModel> CreateBraveSplitTabMenuModel( 
      TabStripModel* tab_strip_model, SplitTabMenuModel::MenuSource source,
      int split_tab_index);
  FRIEND_TEST_ALL_PREFIXES(SideBySideEnabledBrowserTest, SelectTabTest);
  friend class BraveMultiContentsViewMiniToolbar;

```

