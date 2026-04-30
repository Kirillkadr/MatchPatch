### match
```cpp
...
// found in the LICENSE file.
 #include "components/constrained_window/constrained_window_views.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp
#include "components/web_modal/modal_dialog_host.h"

```

### match
```cpp
...
 
 namespace constrained_window { ... 
 
 namespace { ... 
 
 gfx::Rect GetModalDialogBounds(views::Widget* widget,
                               web_modal::ModalDialogHost* dialog_host,
                               const gfx::Size& size) { ... 
if (!host_widget) {
    return gfx::Rect();
  }
 gfx::Point position = dialog_host->GetDialogPosition(size); 
 >>> 
// Align the first row of pixels inside the border. This is the apparent top
 ... } ...  } ...  } ...  
```
### patch
```cpp
  if (auto* widget_delegate = widget->widget_delegate();
      widget_delegate && widget_delegate->has_desired_position_delegate()) {
    position = widget_delegate->get_desired_position();
  };

```

