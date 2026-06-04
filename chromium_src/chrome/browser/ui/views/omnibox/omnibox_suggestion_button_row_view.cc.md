### match
```cpp
...
 
 class OmniboxSuggestionRowButton : public views::MdTextButton { ... 
 
 OmniboxSuggestionRowButton(PressedCallback callback,
                             int context,
                             const gfx::VectorIcon& icon,
                             const gfx::Image& image,
                             OmniboxPopupViewViews* popup_view,
                             OmniboxPopupSelection selection)
      : MdTextButton(std::move(callback),
                     u"",
                     context,
                     /*use_text_color_for_icon=*/false),
        icon_(&icon),
        image_(image),
        popup_view_(popup_view),
        selection_(selection) { ... 
 SetCornerRadius(GetLayoutConstant(LayoutConstant::kToolbarCornerRadius)); 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    (SetCornerRadius(8));

```

