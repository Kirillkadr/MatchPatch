### match
```cpp
...
 #include "chrome/browser/ui/views/frame/browser_frame_view.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/frame/opaque_browser_frame_view.h"

```

### match
```cpp
...
// |type|.
>>> 
 bool ShouldShowWindowTitle(TitlebarType type) const; 
<<< 
// Called when the device enters or exits tablet mode.
 ... 
```
### patch
```cpp
  virtual bool ShouldShowWindowTitle(TitlebarType type) const;

```

### match
```cpp
...
>>>
 void LayoutCaptionButtons(); 
<<< 
...
```
### patch
```cpp
  virtual void LayoutCaptionButtons();

```

### match
```cpp
...
// The bounds of the ClientView.
 gfx::Rect client_view_bounds_; 
 >>> 
// The small icon created from the bitmap image of the window icon.
 ... 
```
### patch
```cpp
  friend class BraveBrowserFrameViewWin;

```

