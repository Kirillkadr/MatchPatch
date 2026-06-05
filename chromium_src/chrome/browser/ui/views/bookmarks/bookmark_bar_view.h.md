### match
```cpp
...
// Returns true if something changed and a LayoutAndPaint() is needed.
>>> 
 bool UpdateOtherAndManagedButtonsVisibility(); 
<<< 
// Updates the visibility of |bookmarks_separator_view_|.
 ... 
```
### patch
```cpp
  friend class BraveBookmarkBarView;               
  virtual bool UpdateOtherAndManagedButtonsVisibility();

```

