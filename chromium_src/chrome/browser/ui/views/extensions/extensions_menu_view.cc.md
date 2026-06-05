### match
```cpp
...
 #include "base/memory/ptr_util.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/extensions/brave_extension_menu_item_view.h"

```

### match
```cpp
...
>>>
 auto 
 * item 
 = 
 new 
 ExtensionMenuItemView 
 ( 
<<< 
...) ...  
```
### patch
```cpp
  auto* item = new BraveExtensionMenuItemView(

```

