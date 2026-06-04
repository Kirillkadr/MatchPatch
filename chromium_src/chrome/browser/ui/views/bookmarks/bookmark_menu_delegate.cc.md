### match
```cpp
...
#include "base/notreached.h"

 #include "base/strings/utf_string_conversions.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/bookmarks/brave_bookmark_context_menu.h"

```

### match
```cpp
...
 
 namespace { ... 
// both IE and FF restrict the max width of a menu.
 const int kMaxMenuWidth = 400; 
 >>> 
size_t GetSubmenuChildCount(const MenuItemView* menu) {
  return menu->HasSubmenu() ? menu->GetSubmenu()->children().size() : 0;
}
 ... } ...  
```
### patch
```cpp
constexpr int kBraveMaxMenuWidth = 500;

```

### match
```cpp
...
>>>
 context_menu_ 
 = 
 std::make_unique<BookmarkContextMenu> 
 ( 
<<< 
...) ...  
```
### patch
```cpp
  context_menu_ = std::make_unique<BraveBookmarkContextMenu>(

```

### match
```cpp
...
 
 int BookmarkMenuDelegate::GetMaxWidthForMenu(MenuItemView* menu) { ... 
>>> 
 return kMaxMenuWidth; 
<<< 
...} ...  
```
### patch
```cpp
  // Chromium limits the width to 400 which causes the menu items to be cut off
  // when displayed in German. Upstream doesn't specify a reason for this size
  // only saying that "IE and FF restrict the max width of a menu". However,
  // MenuDelegate sets the limit to 800 and no other submenu seems to override
  // that value. Update: users indicated that the menu was too wide now, so
  // reduced it to 500, which is enough to fit the German l10n.
  return kBraveMaxMenuWidth;

```

