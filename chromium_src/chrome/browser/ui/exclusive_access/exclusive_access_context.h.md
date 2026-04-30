### match
```cpp
...
 
 # ifndef ... 
 #define CHROME_BROWSER_UI_EXCLUSIVE_ACCESS_EXCLUSIVE_ACCESS_CONTEXT_H_
 
 >>> 
#include "chrome/browser/ui/exclusive_access/exclusive_access_bubble_hide_callback.h"

 ... 
```
### patch
```cpp
#include "base/functional/callback.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ExclusiveAccessContext { ... 
virtual void ExitFullscreen() = 0;
 // Updates the exclusive access bubble. 
 >>> 
virtual void UpdateExclusiveAccessBubble(
      const ExclusiveAccessBubbleParams& params,
      ExclusiveAccessBubbleHideCallback first_hide_callback) = 0;
 ... } ...  
```
### patch
```cpp
  virtual void UpdateExclusiveAccessBubble_ChromiumImpl(
      const ExclusiveAccessBubbleParams& params,
      ExclusiveAccessBubbleHideCallback first_hide_callback) {} 

```

