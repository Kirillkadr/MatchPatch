### match
```cpp
...
 
 WebUIBubbleDialogView::WebUIBubbleDialogView(
    views::View* anchor_view,
    base::WeakPtr<WebUIContentsWrapper> contents_wrapper,
    const std::optional<gfx::Rect>& anchor_rect,
    views::BubbleBorder::Arrow arrow,
    bool autosize)
    : BubbleDialogDelegateView(anchor_view,
                               arrow,
                               views::BubbleBorder::DIALOG_SHADOW,
                               autosize),
      contents_wrapper_(contents_wrapper),
      web_view_(AddChildView(std::make_unique<WebUIBubbleView>(
          contents_wrapper_->web_contents()))),
      bubble_anchor_(anchor_rect) { ... 
SetButtons(static_cast<int>(ui::mojom::DialogButton::kNone));
 set_margins(gfx::Insets()); 
 >>> 
SetLayoutManager(std::make_unique<views::FillLayout>());
 ... } ...  
```
### patch
```cpp
  set_use_round_corners(true);   
  set_corner_radius(16);

```

