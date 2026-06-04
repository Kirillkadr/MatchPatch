### match
```cpp
...
 
 class OmniboxPopupViewViews : public views::View,
                              public OmniboxPopupView,
                              public OmniboxEditModel::Observer { ... 
 friend class OmniboxSuggestionButtonRowBrowserTest; 
 >>> 
 ... } ...  
```
### patch
```cpp
  LocationBarView* location_bar_view() const {
    return location_bar_view_;
  }
  friend class BraveOmniboxPopupViewViews;

```

### match
```cpp
...
// of |location_bar_view_|.
>>> 
 gfx::Rect GetTargetBounds() const; 
<<< 
// Gets the OmniboxHeaderView for match |i|.
 ... 
```
### patch
```cpp
  gfx::Rect virtual GetTargetBounds() const;

```

