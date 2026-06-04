### match
```cpp
...
 #include "base/strings/string_number_conversions.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/omnibox/brave_omnibox_result_view.h"

```

### match
```cpp
...
 
 OmniboxRowView::OmniboxRowView(size_t line, OmniboxPopupViewViews* popup_view)
    : popup_view_(popup_view), line_(line) { ... 
>>> 
 AddChildView(std::make_unique<OmniboxResultView>(popup_view, line)) 
 ; 
<<< 
...} ...  
```
### patch
```cpp
      AddChildView(std::make_unique<BraveOmniboxResultView>(popup_view, line));

```

### match
```cpp
...
 
 gfx::Insets OmniboxRowView::GetInsets() const { ... 
>>> 
 if (result_view_->GetThemeState() == OmniboxPartState::IPH) {
    int LRInsets = OmniboxMatchCellView::kIphOffset;
    return gfx::Insets::TLBR(8, LRInsets, 8, LRInsets);
  } 
 if (result_view_->GetThemeState() == OmniboxPartState::TOOLBELT) {
    return gfx::Insets::TLBR(0, 0, 0, 0);
  } 
 return gfx::Insets::TLBR(0, 0, 0, 16); 
<<< 
...} ...  
```
### patch
```cpp
  return gfx::Insets();

```

