### match
```cpp
...
 #include "base/metrics/histogram_functions.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/omnibox/brave_omnibox_result_view.h"
#include "brave/browser/ui/views/omnibox/brave_rounded_omnibox_results_frame.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 std::optional<gfx::Rect> GetDebugWidgetBounds(
    LocationBarView* location_bar_view,
    int popup_results_height) { ... 
>>> 
 RoundedOmniboxResultsFrame::GetShadowInsets() 
 ; 
<<< 
...} ...  } ...  
```
### patch
```cpp
      BraveRoundedOmniboxResultsFrame::GetShadowInsets();

```

### match
```cpp
...
 
 namespace { ... 
 
 std::optional<gfx::Rect> GetDebugWidgetBounds(
    LocationBarView* location_bar_view,
    int popup_results_height) { ... 
 
 frame_bounds.set_y ( ... 
>>> 
 RoundedOmniboxResultsFrame::GetNonResultSectionHeight() 
 ) 
 ; 
<<< 
...} ...  } ...  
```
### patch
```cpp
                     BraveRoundedOmniboxResultsFrame::GetNonResultSectionHeight());

```

### match
```cpp
...
 
 class OmniboxPopupViewViews::PopupWidget final : public ThemeCopyingWidget { ... 
 
 void InitOmniboxPopup(const views::Widget* parent_widget) { ... 
>>> 
 RoundedOmniboxResultsFrame::OnBeforeWidgetInit(&params, this); 
<<< 
...} ...  } ...  
```
### patch
```cpp
    BraveRoundedOmniboxResultsFrame::OnBeforeWidgetInit(&params, this);

```

### match
```cpp
...
 
 class OmniboxPopupViewViews::PopupWidget final : public ThemeCopyingWidget { ... 
>>> 
 SetContentsView 
 ( 
 std::make_unique<RoundedOmniboxResultsFrame> 
 ( 
<<< 
...) ...  ) ...  } ...  
```
### patch
```cpp
    SetContentsView(std::make_unique<BraveRoundedOmniboxResultsFrame>(

```

### match
```cpp
...
 
 gfx::Rect OmniboxPopupViewViews::GetTargetBounds() const { ... 
// interior between each row of text.
>>> 
 popup_height += RoundedOmniboxResultsFrame::GetNonResultSectionHeight(); 
<<< 
// The rounded popup is always offset the same amount from the omnibox.
 ... } ...  
```
### patch
```cpp
  popup_height += BraveRoundedOmniboxResultsFrame::GetNonResultSectionHeight();

```

### match
```cpp
...
 
 gfx::Rect OmniboxPopupViewViews::GetTargetBounds() const { ... 
 
 content_rect.Inset ( ... 
>>> 
 -RoundedOmniboxResultsFrame::GetLocationBarAlignmentInsets() 
 ) 
 ; 
<<< 
...} ...  
```
### patch
```cpp
      -BraveRoundedOmniboxResultsFrame::GetLocationBarAlignmentInsets());

```

### match
```cpp
...
 
 gfx::Rect OmniboxPopupViewViews::GetTargetBounds() const { ... 
// Finally, expand the widget to accommodate the custom-drawn shadows.
>>> 
 content_rect.Inset(-RoundedOmniboxResultsFrame::GetShadowInsets()); 
<<< 
...} ...  
```
### patch
```cpp
  content_rect.Inset(-BraveRoundedOmniboxResultsFrame::GetShadowInsets());

```

