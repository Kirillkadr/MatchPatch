### match
```cpp
...
 #include "base/notreached.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_opaque_browser_frame_view.h"

```

### match
```cpp
...

>>> 
 : OpaqueBrowserFrameView(widget, browser_view, layout), layout_(layout) 
 { 
<<<
```
### patch
```cpp
: BraveOpaqueBrowserFrameView(widget, browser_view, layout), layout_(layout) {

```

### match
```cpp
...
 
 int BrowserFrameViewLinux::NonClientHitTest(const gfx::Point& point) { ... 
>>> 
 int frame_component = OpaqueBrowserFrameView::NonClientHitTest(point); 
<<< 
// Allow resizing at the top of the caption area. This is only done when
 ... } ...  
```
### patch
```cpp
  int frame_component = BraveOpaqueBrowserFrameView::NonClientHitTest(point);

```

