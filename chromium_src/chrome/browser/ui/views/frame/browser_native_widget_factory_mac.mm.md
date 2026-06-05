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
#include "brave/browser/ui/views/frame/brave_browser_native_widget_mac.h"

```

### match
```cpp
...
 
 BrowserNativeWidget* BrowserNativeWidgetFactory::Create(
    BrowserWidget* browser_widget,
    BrowserView* browser_view) { ... 
>>> 
 return new BrowserNativeWidgetMac(browser_widget, browser_view); 
<<< 
...} ...  
```
### patch
```cpp
  return new BraveBrowserNativeWidgetMac(browser_widget, browser_view);

```

