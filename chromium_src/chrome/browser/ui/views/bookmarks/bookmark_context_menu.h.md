### match
```cpp
...
#include "base/memory/raw_ptr.h"

 #include "base/memory/weak_ptr.h"
 
 >>> 
#include "chrome/browser/ui/bookmarks/bookmark_context_menu_controller.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/toolbar/brave_bookmark_context_menu_controller.h"

```

### match
```cpp
...
>>>
 std::unique_ptr<BookmarkContextMenuController> controller_; 
<<< 
// The parent of dialog boxes opened from the context menu. Uses a WeakPtr
 ... 
```
### patch
```cpp
  std::unique_ptr<BraveBookmarkContextMenuController> controller_;

```

### match
```cpp
...
// Should the menu close when a node is removed.
 bool close_on_remove_; 
 >>> 
 ... 
```
### patch
```cpp
  friend class BraveBookmarkContextMenu;

```

