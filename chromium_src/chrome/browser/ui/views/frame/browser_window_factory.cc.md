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
#include "brave/browser/ui/views/frame/brave_browser_view.h"
#include "brave/browser/ui/views/frame/brave_browser_widget.h"

```

### match
```cpp
...
 
 std::unique_ptr<BrowserWindow, BrowserWindowDeleter>
BrowserWindow::CreateBrowserWindow(Browser* browser,
                                   bool user_gesture,
                                   bool in_tab_dragging) { ... 
// so we don't need to do anything with the pointer.
>>> 
 BrowserView* view = nullptr; 
<<< 
...} ...  
```
### patch
```cpp
  BraveBrowserView* view = nullptr;

```

### match
```cpp
...
 
 std::unique_ptr<BrowserWindow, BrowserWindowDeleter>
BrowserWindow::CreateBrowserWindow(Browser* browser,
                                   bool user_gesture,
                                   bool in_tab_dragging) { ... 
>>> 
 view = new BrowserView(browser); 
<<< 
...} ...  
```
### patch
```cpp
  view = new BraveBrowserView(browser);

```

### match
```cpp
...
 
 std::unique_ptr<BrowserWindow, BrowserWindowDeleter>
BrowserWindow::CreateBrowserWindow(Browser* browser,
                                   bool user_gesture,
                                   bool in_tab_dragging) { ... 
>>> 
 auto browser_widget = std::make_unique<BrowserWidget>(view); 
<<< 
...} ...  
```
### patch
```cpp
  auto browser_widget = std::make_unique<BraveBrowserWidget>(view);

```

