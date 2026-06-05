### match
```cpp
...
 #include "base/scoped_observation.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_browser_view_layout.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/frame/layout/browser_view_layout_delegate.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/frame/layout/browser_view_layout_impl_old.h"

```

### match
```cpp
...
 
 gfx::Size BrowserViewLayout::GetPreferredSize(const views::View* host) const { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp
void BrowserViewLayout::NotifyDialogPositionRequiresUpdate() {
  dialog_host_->NotifyPositionRequiresUpdate();
}

```

