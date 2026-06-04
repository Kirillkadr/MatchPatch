### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/ui/views/frame/browser_frame_view_layout_linux.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/check.h"
#include "base/check_op.h"

```

### match
```cpp
...
 #include "base/i18n/rtl.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/tabs/vertical_tab_utils.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/layout_constants.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/tabs/features.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/frame/opaque_browser_frame_view_layout.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/frame/browser_view.h"
#include "chrome/browser/ui/views/toolbar/toolbar_view.h"

```

### match
```cpp
...
 #include "ui/gfx/geometry/insets.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "ui/views/window/caption_button_layout_constants.h"
#include "ui/views/window/frame_caption_button.h"

```

### match
```cpp
...
 
 int BrowserFrameViewLayoutLinux::NonClientExtraTopThickness() const { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp

void BrowserFrameViewLayoutLinux::SetBoundsForButton(
    views::FrameButton button_id,
    views::Button* button,
    ButtonAlignment align) {
  OpaqueBrowserFrameViewLayout::SetBoundsForButton(button_id, button, align);
  if (!view_) {
    CHECK_IS_TEST();
    return;
  }

  auto* browser = view_->GetBrowserView()->browser();
  DCHECK(browser);

  const bool should_window_caption_buttons_overlap_toolbar =
      tabs::utils::ShouldShowBraveVerticalTabs(browser) &&
      !tabs::utils::ShouldShowWindowTitleForVerticalTabs(browser);
  if (!should_window_caption_buttons_overlap_toolbar) {
    return;
  }

  if (delegate_->GetFrameButtonStyle() ==
      OpaqueBrowserFrameViewLayoutDelegate::FrameButtonStyle::kMdButton) {
    // Synchronize frame button's bounds with toolbar's bounds.
    gfx::Size size = button->GetPreferredSize();
    DCHECK_LT(0, size.width());
    auto* toolbar = view_->GetBrowserView()->toolbar();
    const auto toolbar_height = toolbar->GetPreferredSize().height();
    size.set_height(toolbar_height);
    button->SetPreferredSize(size);
    button->SetSize(size);
    gfx::Point toolbar_origin;
    views::View::ConvertPointToTarget(toolbar, button->parent(),
                                      &toolbar_origin);
    button->SetY(toolbar_origin.y());

    static_cast<views::FrameCaptionButton*>(button)->SetInkDropCornerRadius(
        views::kCaptionButtonInkDropDefaultCornerRadius);
  }
}

```

