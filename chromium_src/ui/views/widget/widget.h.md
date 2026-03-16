### match
```cpp

...
 # ifndef ... 
#include <utility>

 #include <vector>
 
 >>> 
#include "base/callback_list.h"

 ... 
```
### patch
```cpp

#include "build/build_config.h"

```

### match
```cpp

...
 # ifndef ... 
 namespace views { ... 
// Undoes LockPaintAsActive(). This should never be called outside of
 // PaintAsActiveLock destructor. 
 >>> 
void UnlockPaintAsActive();
 ... } ...  
```
### patch
```cpp

  SetWindowTitleVisibility(bool visible);
  void ResetWindowControlsPosition();
  void UpdateWindowTitleColor(SkColor color);

```

