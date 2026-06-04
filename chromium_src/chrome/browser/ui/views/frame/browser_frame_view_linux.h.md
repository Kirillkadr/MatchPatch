### match
```cpp
...
 #include "base/memory/raw_ptr.h"
 
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
 class 
 BrowserFrameViewLinux 
 : 
 public 
 OpaqueBrowserFrameView 
 , 
<<< 
...
```
### patch
```cpp
class BrowserFrameViewLinux : public BraveOpaqueBrowserFrameView,

```

### match
```cpp
...
 
 class BrowserFrameViewLinux : public BraveOpaqueBrowserFrameView,
public ui::WindowButtonOrderObserver { ... 
>>> 
 METADATA_HEADER(BrowserFrameViewLinux, OpaqueBrowserFrameView) 
<<< 
...} ...  
```
### patch
```cpp
  METADATA_HEADER(BrowserFrameViewLinux, BraveOpaqueBrowserFrameView)

```

### match
```cpp
...
 
 class BrowserFrameViewLinux : public BraveOpaqueBrowserFrameView,
public ui::WindowButtonOrderObserver { ... 
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
// Sanity check at compile time.
static_assert(
    std::is_base_of_v<BraveOpaqueBrowserFrameView, BrowserFrameViewLinux>,
    "BrowserFrameViewLinux should be a child of BraveOpaqueBrowserFrameView");


```

