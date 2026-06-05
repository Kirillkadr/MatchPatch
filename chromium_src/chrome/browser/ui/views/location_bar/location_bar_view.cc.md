### match
```cpp
...
 #include "base/trace_event/typed_macros.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "brave/browser/ui/omnibox/brave_omnibox_client_impl.h"
#include "brave/browser/ui/views/omnibox/brave_omnibox_popup_view_views.h"
#include "brave/browser/ui/views/omnibox/brave_omnibox_view_views.h"
#include "brave/browser/ui/views/page_action/brave_page_action_icon_container_view.h"

```

### match
```cpp
...
>>>
 CONTEXT_OMNIBOX_PRIMARY 
 , 
 views::style::STYLE_BODY_4_EMPHASIS 
 ) 
 ; 
<<< 
...
```
### patch
```cpp
CONTEXT_OMNIBOX_PRIMARY, views::style::STYLE_PRIMARY);

```

### match
```cpp
...
 
 void LocationBarView::Init() { ... 
>>> 
 std::make_unique<OmniboxController> 
 ( 
 std::make_unique<ChromeOmniboxClient> 
 ( 
<<< 
/*location_bar=*/
 ... ) ...  ) ...  } ...
```
### patch
```cpp
std::make_unique<OmniboxController>(std::make_unique<BraveOmniboxClientImpl>(

```

### match
```cpp
...
>>>
 auto 
 omnibox_view 
 = 
 std::make_unique<OmniboxViewViews> 
 ( 
<<< 
...) ...
```
### patch
```cpp
auto omnibox_view = std::make_unique<BraveOmniboxViewViews>(

```

### match
```cpp
...
 
 if (!omnibox_popup_view_) { ... 
>>> 
 omnibox_popup_view_ 
 = 
 std::make_unique<OmniboxPopupViewViews> 
 ( 
<<< 
/*omnibox_view=*/
 ... ) ...  } ...
```
### patch
```cpp
omnibox_popup_view_ = std::make_unique<BraveOmniboxPopupViewViews>(

```

### match
```cpp
...
 
 void LocationBarView::Init() { ... 
>>> 
 AddChildView(std::make_unique<PageActionIconContainerView>(params)) 
 ; 
<<< 
...} ...
```
### patch
```cpp
AddChildView(std::make_unique<BravePageActionIconContainerView>(params));

```

### match
```cpp
...
 
!location_icon_view_->ShouldShowLabel() &&
                !ShouldShowKeywordBubble();
 >>>
```
### patch
```cpp
icon_left = GetLayoutConstant(LayoutConstant::kLocationBarElementPadding);
  if (text_left == 0 && !location_icon_view_->ShouldShowLabel()) {
    text_left = 5;
  }

```

### match
```cpp
...

 
 if (selected_keyword_view_->GetKeyword() != keyword) { ... 
 } 
 >>>
```
### patch
```cpp
}
  else if (GetSearchPromotionButton() && /* NOLINT */
           GetSearchPromotionButton()->GetVisible()) {
    leading_decorations.AddDecoration(vertical_padding, location_height,
                                      false, kLeadingDecorationMaxFraction,
                                      /*intra_item_padding=*/0, 0,
                                      GetSearchPromotionButton());

```

### match
```cpp
...
 : 
 trailing_decorations_edge_padding 
 ; 
 >>> 
 ... 
```
### patch
```cpp
auto right_most_trailing_views = GetRightMostTrailingViews();
  for (auto* item : base::Reversed(right_most_trailing_views)) {
    add_trailing_decoration(
        item, /*intra_item_padding=*/0,
        /*edge_padding=*/trailing_decorations_edge_padding);
  }

```

### match
```cpp
...
clear_all_button_, /*intra_item_padding=*/0,
                          
 /*edge_padding=*/ 
 trailing_decorations_edge_padding 
 ) 
 ; 
 >>> 
 ... 
```
### patch
```cpp
  auto left_most_trailing_views = GetLeftMostTrailingViews();
  for (auto* item : base::Reversed(left_most_trailing_views)) {
    add_trailing_decoration(
        item, /*intra_item_padding=*/0,
        /*edge_padding=*/trailing_decorations_edge_padding);
  }

```

### match
```cpp
...
 
 page_actions::PageActionController* LocationBarView::GetPageActionController() { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp
views::View* LocationBarView::GetSearchPromotionButton() const {
  return nullptr;
}

std::vector<views::View*> LocationBarView::GetRightMostTrailingViews() {
  return std::vector<views::View*>();
}

std::vector<views::View*> LocationBarView::GetLeftMostTrailingViews() {
  return std::vector<views::View*>();
}



```

