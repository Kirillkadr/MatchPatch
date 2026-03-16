### match
```cpp

...
 namespace views { ... 
 int BubbleFrameView::GetFrameWidthForClientWidth(int client_width) const { ...   >>> 
 static_cast<int>(ui::mojom::DialogButton::kNone) 
 ;  <<< ... } ...  } ...  
```
### patch
```cpp

                             static_cast<int>(ui::mojom::DialogButton::kNone) && !dialog_delegate->should_ignore_snapping();

```

