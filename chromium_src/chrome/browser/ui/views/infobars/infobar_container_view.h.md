### match
```cpp
...
 #include "base/memory/raw_ptr.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "components/infobars/core/infobar_container.h"

```

### match
```cpp
...
 
 class InfoBarContainerView : public views::AccessiblePaneView,
                             public infobars::InfoBarContainerWithPriority { ... 
 size_t position 
 ) 
 override 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  friend class BraveInfoBarContainerView;   

```

