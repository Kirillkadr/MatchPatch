### match
```cpp
...
 #include <utility>
 
 >>> 
 ... 
```
### patch
```cpp
#include <dwmapi.h>
#include "base/check.h"

```

### match
```cpp
...
 #include "base/task/thread_pool.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/win/windows_types.h"

```

### match
```cpp
...
 #include "base/win/windows_version.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/brave_ui_features.h"

```

### match
```cpp
...
 #include "chrome/browser/themes/theme_service_factory.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/color/chrome_color_id.h"

```

### match
```cpp
...
 #include "content/public/browser/browser_thread.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "skia/ext/skia_utils_win.h"

```

### match
```cpp
...
>>>
 BrowserDesktopWindowTreeHostWin::BrowserDesktopWindowTreeHostWin 
 ( 
<<< 
...) ...  
```
### patch
```cpp
BrowserDesktopWindowTreeHostWin_ChromiumImpl::BrowserDesktopWindowTreeHostWin_ChromiumImpl(

```

### match
```cpp
...
>>>
 BrowserDesktopWindowTreeHostWin::~BrowserDesktopWindowTreeHostWin() = default; 
<<< 
...
```
### patch
```cpp
BrowserDesktopWindowTreeHostWin_ChromiumImpl::~BrowserDesktopWindowTreeHostWin_ChromiumImpl() = default;

```

### match
```cpp
...
>>>
 views::NativeMenuWin 
 * BrowserDesktopWindowTreeHostWin::GetSystemMenu() 
 { 
<<< 
...} ...  
```
### patch
```cpp

views::NativeMenuWin* BrowserDesktopWindowTreeHostWin_ChromiumImpl::GetSystemMenu() {

```

### match
```cpp
...
>>>
 BrowserDesktopWindowTreeHostWin::AsDesktopWindowTreeHost() 
 { 
<<< 
...} ...  
```
### patch
```cpp
BrowserDesktopWindowTreeHostWin_ChromiumImpl::AsDesktopWindowTreeHost() {

```

### match
```cpp
...
>>>
 bool 
 BrowserDesktopWindowTreeHostWin::UsesNativeSystemMenu() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool BrowserDesktopWindowTreeHostWin_ChromiumImpl::UsesNativeSystemMenu() const {

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::Init 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::Init(

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::Show 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::Show(

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::HandleWindowMinimizedOrRestored 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::HandleWindowMinimizedOrRestored(

```

### match
```cpp
...
>>>
 std::string 
 BrowserDesktopWindowTreeHostWin::GetWorkspace() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
std::string BrowserDesktopWindowTreeHostWin_ChromiumImpl::GetWorkspace() const {

```

### match
```cpp
...
>>>
 int 
 BrowserDesktopWindowTreeHostWin::GetInitialShowState() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
int BrowserDesktopWindowTreeHostWin_ChromiumImpl::GetInitialShowState() const {

```

### match
```cpp
...
>>>
 bool 
 BrowserDesktopWindowTreeHostWin::GetClientAreaInsets 
 ( 
<<< 
...) ...  
```
### patch
```cpp
bool BrowserDesktopWindowTreeHostWin_ChromiumImpl::GetClientAreaInsets(

```

### match
```cpp
...
>>>
 bool 
 BrowserDesktopWindowTreeHostWin::GetDwmFrameInsetsInPixels 
 ( 
<<< 
...) ...  
```
### patch
```cpp
bool BrowserDesktopWindowTreeHostWin_ChromiumImpl::GetDwmFrameInsetsInPixels(

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::HandleCreate() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::HandleCreate() {

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::HandleDestroying() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::HandleDestroying() {

```

### match
```cpp
...
>>>
 bool 
 BrowserDesktopWindowTreeHostWin::PreHandleMSG 
 ( 
 UINT message 
 , 
<<< 
...) ...  
```
### patch
```cpp
bool BrowserDesktopWindowTreeHostWin_ChromiumImpl::PreHandleMSG(UINT message,

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::PostHandleMSG 
 ( 
 UINT message 
 , 
<<< 
...) ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::PostHandleMSG(UINT message,

```

### match
```cpp
...
>>>
 views::FrameMode 
 BrowserDesktopWindowTreeHostWin::GetFrameMode() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
views::FrameMode BrowserDesktopWindowTreeHostWin_ChromiumImpl::GetFrameMode() const {

```

### match
```cpp
...
>>>
 bool 
 BrowserDesktopWindowTreeHostWin::ShouldUseNativeFrame() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool BrowserDesktopWindowTreeHostWin_ChromiumImpl::ShouldUseNativeFrame() const {

```

### match
```cpp
...
>>>
 bool 
 BrowserDesktopWindowTreeHostWin::ShouldWindowContentsBeTransparent 
 () 
<<< 
...
```
### patch
```cpp
bool BrowserDesktopWindowTreeHostWin_ChromiumImpl::ShouldWindowContentsBeTransparent()

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::ClientDestroyedWidget() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::ClientDestroyedWidget() {

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::OnProfileAvatarChanged 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::OnProfileAvatarChanged(

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::OnProfileAdded 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::OnProfileAdded(

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::OnProfileWasRemoved 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::OnProfileWasRemoved(

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::UpdateWorkspace() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::UpdateWorkspace() {

```

### match
```cpp
...
 
 virtual_desktop_helper_->UpdateWindowDesktopId ( ... 
>>> 
 base::BindOnce 
 ( 
 &BrowserDesktopWindowTreeHostWin::OnHostWorkspaceChanged 
 , 
<<< 
...) ...  ) ...  
```
### patch
```cpp
      base::BindOnce(&BrowserDesktopWindowTreeHostWin_ChromiumImpl::OnHostWorkspaceChanged,

```

### match
```cpp
...
>>>
 void 
 BrowserDesktopWindowTreeHostWin::SetWindowIcon(bool badged) 
 { 
<<< 
// Hold onto the previous icon so that the currently displayed
 ... } ...  
```
### patch
```cpp
void BrowserDesktopWindowTreeHostWin_ChromiumImpl::SetWindowIcon(bool badged) {

```

### match
```cpp
...
////////////////////////////////////////////////////////////////////////////////
 // BrowserDesktopWindowTreeHost, public: 
 >>> 
// static
 ... 
```
### patch
```cpp
// static
BrowserDesktopWindowTreeHost*

bool BrowserDesktopWindowTreeHostWin::PreHandleMSG(UINT message,
                                                   WPARAM w_param,
                                                   LPARAM l_param,
                                                   LRESULT* result) {
  switch (message) {
    case WM_NCCREATE: {
      // Cloak the window on creation to prevent a white flash.
      if (!is_cloacked_ && base::FeatureList::IsEnabled(
                               features::kBraveWorkaroundNewWindowFlash)) {
        const BOOL cloak = TRUE;
        is_cloacked_ = SUCCEEDED(DwmSetWindowAttribute(GetHWND(), DWMWA_CLOAK,
                                                       &cloak, sizeof(cloak)));
      }
      break;
    }
    case WM_NCPAINT: {
      // If the window is cloacked, fill it with the toolbar color and uncloak.
      if (is_cloacked_ && base::FeatureList::IsEnabled(
                              features::kBraveWorkaroundNewWindowFlash)) {
        HWND hwnd = GetHWND();
        HDC dc = GetWindowDC(hwnd);
        RECT window_rect;
        GetWindowRect(hwnd, &window_rect);
        const RECT fill_rect = {
            0,
            0,
            window_rect.right - window_rect.left,
            window_rect.bottom - window_rect.top,
        };

        SkColor bg_color = GetToolbarColor();
        HBRUSH brush = ::CreateSolidBrush(skia::SkColorToCOLORREF(bg_color));
        ::FillRect(dc, &fill_rect, brush);
        ::DeleteObject(brush);
        ::ReleaseDC(hwnd, dc);
        const BOOL cloak = FALSE;
        is_cloacked_ = !SUCCEEDED(
            DwmSetWindowAttribute(hwnd, DWMWA_CLOAK, &cloak, sizeof(cloak)));
      }
      break;
    }
  }
  return BrowserDesktopWindowTreeHostWin_ChromiumImpl::PreHandleMSG(
      message, w_param, l_param, result);
}

SkColor BrowserDesktopWindowTreeHostWin::GetBackgroundColor(
    SkColor requested_color) const {
  if (requested_color == SK_ColorTRANSPARENT ||
      !base::FeatureList::IsEnabled(features::kBraveWorkaroundNewWindowFlash)) {
    return requested_color;
  }

  return GetToolbarColor();
}

SkColor BrowserDesktopWindowTreeHostWin::GetToolbarColor() const {
  CHECK(base::FeatureList::IsEnabled(features::kBraveWorkaroundNewWindowFlash));
  return GetWidget()->GetColorProvider()->GetColor(kColorToolbar);
}


```

