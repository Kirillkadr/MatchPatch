### match
```cpp
...
 
 void MultiContentsResizeArea::OnGestureEvent(ui::GestureEvent* event) { ... 
 
 if (!is_resizing() && event->type() == ui::EventType::kGestureTap &&
      event->details().tap_count() == 2) { ... 
>>> 
 multi_contents_view_->OnSwap(); 
<<< 
...} ...  } ...  
```
### patch
```cpp
    multi_contents_view_->ResetResizeArea();

```

### match
```cpp
...
 
 void MultiContentsResizeArea::OnMouseReleased(const ui::MouseEvent& event) { ... 
 
 if (!is_resizing() && event.IsOnlyLeftMouseButton() &&
      event.GetClickCount() == 2) { ... 
>>> 
 multi_contents_view_->OnSwap(); 
<<< 
...} ...  } ...  
```
### patch
```cpp
    multi_contents_view_->ResetResizeArea();

```

