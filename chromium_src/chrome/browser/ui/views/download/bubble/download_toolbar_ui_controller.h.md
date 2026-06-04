### match
```cpp
...
 class ProfileBrowserCollection 
 ; 
 >>> 
// DownloadToolbarUIController is a controller for the downloads button shown in
 ...
```
### patch
```cpp
class DownloadToolbarUIController;
using DownloadToolbarUIController_BraveImpl = DownloadToolbarUIController;

```

### match
```cpp
...
#ifndef CHROME_BROWSER_UI_VIEWS_DOWNLOAD_BUBBLE_DOWNLOAD_TOOLBAR_UI_CONTROLLER_H_
#define CHROME_BROWSER_UI_VIEWS_DOWNLOAD_BUBBLE_DOWNLOAD_TOOLBAR_UI_CONTROLLER_H_

#include <string>

#include "base/memory/raw_ptr.h"
#include "base/scoped_observation.h"
#include "base/timer/timer.h"
#include "chrome/browser/download/download_ui_model.h"
#include "chrome/browser/ui/browser_window/public/browser_collection_observer.h"
#include "chrome/browser/ui/browser_window/public/browser_window_interface.h"
#include "chrome/browser/ui/download/download_bubble_row_list_view_info.h"
#include "chrome/browser/ui/download/download_display.h"
#include "chrome/browser/ui/views/download/bubble/download_bubble_navigation_handler.h"
#include "chrome/browser/ui/views/frame/immersive_mode_controller.h"
#include "components/offline_items_collection/core/offline_item.h"
#include "ui/base/metadata/metadata_header_macros.h"
#include "ui/base/unowned_user_data/scoped_unowned_user_data.h"
#include "ui/events/event_observer.h"
#include "ui/views/bubble/bubble_dialog_delegate_view.h"
#include "ui/views/widget/widget_observer.h"

namespace offline_items_collection {
struct ContentId;
}

namespace views {
class EventMonitor;
class Widget;
}  // namespace views

class BrowserView;
class DownloadDisplayController;
class DownloadBubbleContentsView;
class DownloadBubbleUIController;
class ProfileBrowserCollection;
class DownloadToolbarUIController;
using DownloadToolbarUIController_BraveImpl = DownloadToolbarUIController;
// DownloadToolbarUIController is a controller for the downloads button shown in
// the trusted area of the toolbar. This controller manages state, animations,
// and badges for the button. The icon is made visible when pinned or when
// downloads are in progress or when a download was initiated in the past 1
// hour.

>>> 
 class 
 DownloadToolbarUIController 
<<< 
...
```
### patch
```cpp
class DownloadToolbarUIController_ChromiumImpl

```

### match
```cpp
...
 
 class DownloadToolbarUIController_ChromiumImpl
: public DownloadDisplay,
      public DownloadBubbleNavigationHandler,
      public BrowserCollectionObserver,
      public DownloadBubbleRowListViewInfoObserver { ... 
>>> 
 DECLARE_USER_DATA(DownloadToolbarUIController); 
<<< 
...} ...
```
### patch
```cpp
DECLARE_USER_DATA(DownloadToolbarUIController_ChromiumImpl);

```

### match
```cpp
...
>>>
 static DownloadToolbarUIController* From(BrowserWindowInterface* browser); 
<<< 
// Identifies the bubble dialog widget for testing.
 ...
```
### patch
```cpp
  static DownloadToolbarUIController_ChromiumImpl* From(BrowserWindowInterface* browser);


```

### match
```cpp
...
>>>
 explicit DownloadToolbarUIController(BrowserView* browser_view); 
 DownloadToolbarUIController(const DownloadToolbarUIController&) = delete; 
 DownloadToolbarUIController 
 & operator=(const DownloadToolbarUIController&) 
 = 
<<< 
...
```
### patch
```cpp
explicit DownloadToolbarUIController_ChromiumImpl(BrowserView* browser_view);
  DownloadToolbarUIController_ChromiumImpl(const DownloadToolbarUIController_ChromiumImpl&) = delete;
  DownloadToolbarUIController_ChromiumImpl& operator=(const DownloadToolbarUIController_ChromiumImpl&) =

```

### match
```cpp
...
 
 class DownloadToolbarUIController_ChromiumImpl
: public DownloadDisplay,
      public DownloadBubbleNavigationHandler,
      public BrowserCollectionObserver,
      public DownloadBubbleRowListViewInfoObserver { ... 
>>> 
 ~DownloadToolbarUIController() override; 
<<< 
// Create the DownloadDisplayController, this must be called once the
 ... } ...
```
### patch
```cpp
~DownloadToolbarUIController_ChromiumImpl() override;

```

### match
```cpp
...
 >>> 
void CreateBubbleDialogDelegate(); ...
```
### patch
```cpp
friend DownloadToolbarUIController_BraveImpl;

```

### match
```cpp
...
// or normal state.
>>> 
 void UpdateIconDormant(); 
<<< 
// DownloadBubbleRowListViewInfoObserver:
 ... 
```
### patch
```cpp
  virtual void UpdateIconDormant();

```

### match
```cpp
...
 
 class DownloadToolbarUIController_ChromiumImpl
: public DownloadDisplay,
      public DownloadBubbleNavigationHandler,
      public BrowserCollectionObserver,
      public DownloadBubbleRowListViewInfoObserver { ... 
>>> 
 ui::ScopedUnownedUserData<DownloadToolbarUIController> 
<<< 
...} ...  
```
### patch
```cpp
  ui::ScopedUnownedUserData<DownloadToolbarUIController_ChromiumImpl>

```

### match
```cpp
...
>>>
 base::WeakPtrFactory<DownloadToolbarUIController> weak_factory_{this}; 
<<< 
...
```
### patch
```cpp
  base::WeakPtrFactory<DownloadToolbarUIController_ChromiumImpl> weak_factory_{this};

```

### match
```cpp
...
 
 class DownloadToolbarUIController_ChromiumImpl
: public DownloadDisplay,
      public DownloadBubbleNavigationHandler,
      public BrowserCollectionObserver,
      public DownloadBubbleRowListViewInfoObserver { ... 
 } 
 ; 
 >>> 
 ... 
```
### patch
```cpp
class DownloadToolbarUIController
    : public DownloadToolbarUIController_ChromiumImpl {
 public:
  using DownloadToolbarUIController_ChromiumImpl::
      DownloadToolbarUIController_ChromiumImpl;

  void UpdateIcon() override;

 private:
  bool HasInsecureDownloads();
};

```

