### match
```cpp
...
#include "base/memory/raw_ptr.h"

 #include "base/timer/elapsed_timer.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/toolbar/brave_bookmark_sub_menu_model.h"

```

### match
```cpp
...
#include "chrome/app/chrome_command_ids.h"

 #include "chrome/browser/ui/safety_hub/safety_hub_constants.h"
 
 >>> 
#include "components/prefs/pref_change_registrar.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/ui/toolbar/bookmark_sub_menu_model.h"

```

### match
```cpp
...
>>>
 class BookmarkSubMenuModel 
 ; 
<<< 
class Browser
 ... 
```
### patch
```cpp
class BraveBookmarkSubMenuModel;

```

### match
```cpp
...
>>>
 BookmarkSubMenuModel 
 * bookmark_sub_menu_model() const 
 { 
<<< 
return bookmark_sub_menu_model_.get();
 ... } ...  
```
### patch
```cpp
  BraveBookmarkSubMenuModel* bookmark_sub_menu_model() const {

```

### match
```cpp
...
 
 class AppMenuModel : public ui::SimpleMenuModel,
                     public user_education::HighlightingSimpleMenuModelDelegate,
                     public ui::ButtonMenuItemModel::Delegate { ... 
void CreateFindAndEditSubMenu();
 // Appends a zoom menu (without separators). 
 >>> 
void CreateZoomMenu();
 ... } ...  
```
### patch
```cpp
  std::vector<std::unique_ptr<SimpleMenuModel>>& sub_menus() {
    return sub_menus_;
  }

```

### match
```cpp
...
// Bookmark submenu.
>>> 
 std::unique_ptr<BookmarkSubMenuModel> bookmark_sub_menu_model_; 
<<< 
// Other submenus.
 ... 
```
### patch
```cpp
  std::unique_ptr<BraveBookmarkSubMenuModel> bookmark_sub_menu_model_;

```

