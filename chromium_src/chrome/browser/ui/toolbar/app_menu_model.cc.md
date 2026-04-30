### match
```cpp
...
#include "base/strings/string_util.h"

 #include "base/strings/utf_string_conversions.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/toolbar/brave_bookmark_sub_menu_model.h"
#include "brave/browser/ui/toolbar/brave_recent_tabs_sub_menu_model.h"
#include "brave/grit/brave_generated_resources.h"

```

### match
```cpp
...
 
 void AppMenuModel::Build() { ... 
 
 if (!browser_->profile()->IsOffTheRecord()) { ...   >>> 
 std::make_unique<RecentTabsSubMenuModel>(provider_, browser_) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
        std::make_unique<BraveRecentTabsSubMenuModel>(provider_, browser_);

```

### match
```cpp
...
 
 void AppMenuModel::Build() { ... 
 
 if (!browser_->profile()->IsGuestSession()) { ...   >>> 
 std::make_unique<BookmarkSubMenuModel>(this, browser_) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
        std::make_unique<BraveBookmarkSubMenuModel>(this, browser_);

```

 