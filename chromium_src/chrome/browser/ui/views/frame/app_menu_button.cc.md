### match
```cpp
...
 #include "base/types/pass_key.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/toolbar/brave_app_menu.h"

```

### match
```cpp
...
>>>
 menu_ 
 = 
 std::make_unique<AppMenu> 
 ( 
<<< 
...) ...  
```
### patch
```cpp
  menu_ = std::make_unique<BraveAppMenu>(

```

