### match
```cpp
...
#include "base/no_destructor.h"

 #include "base/strings/utf_string_conversions.h"
 
 >>> 
#include "chrome/app/chrome_command_ids.h"

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
 : 
 controller_ 
 ( 
 new 
 BookmarkContextMenuController 
 ( 
<<< 
parent_widget ? parent_widget->GetNativeWindow()
                        : gfx::NativeWindow()
 ... ) ...  ) ...  
```
### patch
```cpp
    : controller_(new BraveBookmarkContextMenuController(

```

