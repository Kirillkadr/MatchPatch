### match
```cpp
...
 
 std::unique_ptr<views::Background> OmniboxResultView::GetPopupCellBackground(
    const views::View* view,
    OmniboxPartState part_state) { ... 
>>> 
 const float half_row_height = OmniboxMatchCellView::kRowHeight / 2; 
<<< 
...} ...  
```
### patch
```cpp
  const float half_row_height = OmniboxMatchCellView::kRowHeight * 0 / 2;

```

