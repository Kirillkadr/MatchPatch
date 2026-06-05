### match
```cpp
...
 class VirtualDesktopHelper 
 ; 
 >>> 
 ...
```
### patch
```cpp
class BrowserDesktopWindowTreeHostWin;
using BrowserDesktopWindowTreeHostWin_BraveImpl =
    BrowserDesktopWindowTreeHostWin;

```

### match
```cpp
...
#ifndef CHROME_BROWSER_UI_VIEWS_FRAME_BROWSER_DESKTOP_WINDOW_TREE_HOST_WIN_H_
#define CHROME_BROWSER_UI_VIEWS_FRAME_BROWSER_DESKTOP_WINDOW_TREE_HOST_WIN_H_

#include <shobjidl.h>

#include <wrl/client.h>

#include <memory>
#include <string>

#include "base/memory/raw_ptr.h"
#include "base/memory/weak_ptr.h"
#include "base/scoped_observation.h"
#include "base/task/sequenced_task_runner.h"
#include "base/win/scoped_gdi_object.h"
#include "chrome/browser/profiles/profile_attributes_storage.h"
#include "chrome/browser/ui/views/frame/browser_desktop_window_tree_host.h"
#include "ui/base/mojom/window_show_state.mojom-forward.h"
#include "ui/views/widget/desktop_aura/desktop_window_tree_host_win.h"

class BrowserWidget;
class BrowserView;
class BrowserWindowPropertyManager;
class VirtualDesktopHelper;
class BrowserDesktopWindowTreeHostWin;
using BrowserDesktopWindowTreeHostWin_BraveImpl =
    BrowserDesktopWindowTreeHostWin;

namespace views {
class DesktopNativeWidgetAura;
class NativeMenuWin;
}  // namespace views


>>> 
 class 
 BrowserDesktopWindowTreeHostWin 
<<< 
...
```
### patch
```cpp
class BrowserDesktopWindowTreeHostWin_ChromiumImpl

```

### match
```cpp
...
 
 namespace views {
class DesktopNativeWidgetAura;
class NativeMenuWin;
}  // namespace views

class BrowserDesktopWindowTreeHostWin_ChromiumImpl
    : public BrowserDesktopWindowTreeHost,
      public views::DesktopWindowTreeHostWin,
      public ProfileAttributesStorage::Observer {
 public:
>>> 
 BrowserDesktopWindowTreeHostWin 
 ( 
<<< 
...
```
### patch
```cpp
BrowserDesktopWindowTreeHostWin_ChromiumImpl(

```

### match
```cpp
...
 
 class BrowserDesktopWindowTreeHostWin_ChromiumImpl
: public BrowserDesktopWindowTreeHost,
      public views::DesktopWindowTreeHostWin,
      public ProfileAttributesStorage::Observer { ... 
>>> 
 BrowserDesktopWindowTreeHostWin(const BrowserDesktopWindowTreeHostWin&) 
 = 
<<< 
...} ...  
```
### patch
```cpp
  BrowserDesktopWindowTreeHostWin_ChromiumImpl(const BrowserDesktopWindowTreeHostWin_ChromiumImpl&) =

```

### match
```cpp
...
 
 class BrowserDesktopWindowTreeHostWin_ChromiumImpl
: public BrowserDesktopWindowTreeHost,
      public views::DesktopWindowTreeHostWin,
      public ProfileAttributesStorage::Observer { ... 
>>> 
 BrowserDesktopWindowTreeHostWin& operator=(
      const BrowserDesktopWindowTreeHostWin&) = delete; 
 ~BrowserDesktopWindowTreeHostWin() override; 
<<< 
...} ...  
```
### patch
```cpp
  BrowserDesktopWindowTreeHostWin_ChromiumImpl& operator=(
      const BrowserDesktopWindowTreeHostWin_ChromiumImpl&) = delete;
  ~BrowserDesktopWindowTreeHostWin_ChromiumImpl() override;

```

### match
```cpp
...
// WindowTreeHost of its value.
 void UpdateWorkspace(); 
 >>> 
 ... 
```
### patch
```cpp
  friend BrowserDesktopWindowTreeHostWin_BraveImpl;

```

### match
```cpp
...
>>>
 base::WeakPtrFactory<BrowserDesktopWindowTreeHostWin> weak_factory_{this}; 
<<< 
...
```
### patch
```cpp
  base::WeakPtrFactory<BrowserDesktopWindowTreeHostWin_ChromiumImpl> weak_factory_{this};
};

class BrowserDesktopWindowTreeHostWin
    : public BrowserDesktopWindowTreeHostWin_ChromiumImpl {
 public:
  using BrowserDesktopWindowTreeHostWin_ChromiumImpl::
      BrowserDesktopWindowTreeHostWin_ChromiumImpl;

 private:
  bool PreHandleMSG(UINT message,
                    WPARAM w_param,
                    LPARAM l_param,
                    LRESULT* result) override;

  // Returns the optionally modified background color to correctly match the
  // toolbar color in dark/private browsing modes.
  SkColor GetBackgroundColor(SkColor requested_color) const override;

  SkColor GetToolbarColor() const;

  bool is_cloacked_ = false;

```

