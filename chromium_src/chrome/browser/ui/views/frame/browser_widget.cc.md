### match
```cpp
...
 #include "base/metrics/user_metrics.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_system_menu_model_builder.h"

```

### match
```cpp
...
 
 if (!menu_model_builder_.get()) { ... 
>>> 
 menu_model_builder_ 
 = 
 std::make_unique<SystemMenuModelBuilder> 
 ( 
<<< 
...) ...  } ...  
```
### patch
```cpp
    menu_model_builder_ = std::make_unique<BraveSystemMenuModelBuilder>(

```

