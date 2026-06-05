### match
```cpp
...
// found in the LICENSE file.
 #include <memory>
 
 >>> 
 ...
```
### patch
```cpp
#include <type_traits>
#include "brave/browser/ui/views/frame/brave_opaque_browser_frame_view.h"

```

### match
```cpp
...
 #if 
 BUILDFLAG(IS_WIN) 
 >>> 
#include "chrome/browser/ui/views/frame/browser_frame_view_win.h"

 ...
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_browser_frame_view_win.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/frame/browser_frame_view_win.h"
 
 >>> 
 ...
```
### patch
```cpp
#define BrowserFrameViewWin BraveBrowserFrameViewWin

```

### match
```cpp
...
 #if 
 BUILDFLAG(IS_LINUX) 
 >>> 
#include "chrome/browser/ui/views/frame/browser_frame_view_layout_linux.h"

 ...
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_browser_frame_view_linux_native.h"

```

### match
```cpp
...
 #include "ui/linux/window_frame_provider.h"
 
 >>> 
 ... 
```
### patch
```cpp
#define BrowserFrameViewLinuxNative BraveBrowserFrameViewLinuxNative

```

### match
```cpp
...
>>>
 std::unique_ptr<OpaqueBrowserFrameView> 
 CreateOpaqueBrowserFrameViewLinux 
 ( 
<<< 
...) ...  
```
### patch
```cpp
std::unique_ptr<BraveOpaqueBrowserFrameView> CreateOpaqueBrowserFrameViewLinux(

```

### match
```cpp
...
>>>
 auto 
 opaque_browser_view 
 = 
 std::make_unique<OpaqueBrowserFrameView> 
 ( 
<<< 
...) ...  
```
### patch
```cpp
  auto opaque_browser_view = std::make_unique<BraveOpaqueBrowserFrameView>(

```

### match
```cpp
...
 
 namespace chrome { ... 
 } 
 // namespace chrome 
 >>> 
 ... 
```
### patch
```cpp

#if BUILDFLAG(IS_LINUX)
#undef BrowserFrameViewLinuxNative

// A sanity check for our macro
static_assert(
    std::is_same_v<std::unique_ptr<BraveOpaqueBrowserFrameView>,
                   std::invoke_result_t<
                       decltype(chrome::CreateOpaqueBrowserFrameViewLinux),
                       BrowserWidget*,
                       BrowserView*>>,
    "CreateOpaqueBrowserFrameViewLinux is not returning "
    "BraveOpaqueBrowserFrameView");
#endif  // BUILDFLAG(IS_LINUX)

#if BUILDFLAG(IS_WIN)
#undef BrowserFrameViewWin
#endif
```

