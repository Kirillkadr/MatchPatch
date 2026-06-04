### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/ui/views/overlay/simple_overlay_window_image_button.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "ui/display/display.h"
#include "ui/gfx/image/image_skia.h"
#include "ui/views/view.h"

```

### match
```cpp
...
 
 void SimpleOverlayWindowImageButton::UpdateImage() { ... 
>>> 
 const int icon_size = std::max(0, width() - (2 * kPipWindowIconPadding)); 
<<< 
...} ...  
```
### patch
```cpp
  const int icon_size = std::max(0, icon_size_.value_or(width()) - (2 * kPipWindowIconPadding));

```

