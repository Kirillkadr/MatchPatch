### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_browser_frame_view_mac.h"

```

### match
```cpp
...
 
 namespace chrome { ... 
 
 std::unique_ptr<BrowserFrameView> CreateBrowserFrameView(
    BrowserWidget* frame,
    BrowserView* browser_view) { ... 
>>> 
 return std::make_unique<BrowserFrameViewMac>(frame, browser_view); 
<<< 
...} ...  } ...  
```
### patch
```cpp
  return std::make_unique<BraveBrowserFrameViewMac>(frame, browser_view);

```

