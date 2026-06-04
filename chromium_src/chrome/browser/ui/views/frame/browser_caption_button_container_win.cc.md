### match
```cpp
...
 #include "base/win/windows_version.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_browser_frame_view_win.h"
#include "brave/browser/ui/views/tabs/vertical_tab_utils.h"
#include "chrome/browser/profiles/profile.h"

```

### match
```cpp
...
>>>
 BrowserCaptionButtonContainer::BrowserCaptionButtonContainer 
 ( 
<<< 
...) ...  
```
### patch
```cpp
BrowserCaptionButtonContainer_ChromiumImpl::BrowserCaptionButtonContainer_ChromiumImpl(

```

### match
```cpp
...
>>>
 BrowserCaptionButtonContainer::~BrowserCaptionButtonContainer() = default; 
<<< 
...
```
### patch
```cpp
BrowserCaptionButtonContainer_ChromiumImpl::~BrowserCaptionButtonContainer_ChromiumImpl() = default;

```

### match
```cpp
...
>>>
 int 
 BrowserCaptionButtonContainer::NonClientHitTest 
 ( 
<<< 
...) ...  
```
### patch
```cpp

int BrowserCaptionButtonContainer_ChromiumImpl::NonClientHitTest(

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer::OnWindowControlsOverlayEnabledChanged() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::OnWindowControlsOverlayEnabledChanged() {

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer::OnThemeChanged() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::OnThemeChanged() {

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer::ResetWindowControls() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::ResetWindowControls() {

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer::AddedToWidget() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::AddedToWidget() {

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer::RemovedFromWidget() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::RemovedFromWidget() {

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer::OnWidgetBoundsChanged 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::OnWidgetBoundsChanged(

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer::UpdateButtons() 
 { 
 if 
 (!ShouldBrowserCustomDrawTitlebar(frame_view_->GetBrowserView())) 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::UpdateButtons() {
  if (!(static_cast<BraveBrowserFrameViewWin*>(frame_view_.get())
       ->ShouldCaptionButtonsBeDrawnOverToolbar() ||
   ShouldBrowserCustomDrawTitlebar(frame_view_->GetBrowserView()))) {

```

### match
```cpp
...
>>>
 void 
 BrowserCaptionButtonContainer 
 :: 
<<< 
...
```
### patch
```cpp
void BrowserCaptionButtonContainer_ChromiumImpl::

```

### match
```cpp
...
 
 void BrowserCaptionButtonContainer_ChromiumImpl::
UpdateButtonToolTipsForWindowControlsOverlay() { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp
BEGIN_METADATA(BrowserCaptionButtonContainer_ChromiumImpl)
END_METADATA

BrowserCaptionButtonContainer::BrowserCaptionButtonContainer(
    BrowserFrameViewWin* frame_view)
    : BrowserCaptionButtonContainer_ChromiumImpl(frame_view),
      frame_view_(frame_view) {
}

BrowserCaptionButtonContainer::~BrowserCaptionButtonContainer() = default;


```

