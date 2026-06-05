### match
```cpp
...
 
 class ContentsContainerView : public views::View,
                              public views::LayoutDelegate,
                              public views::ViewObserver { ... 
>>> 
 void 
 UpdateBorderAndOverlay 
 ( 
 bool is_in_split 
 , 
<<< 
...) ...  } ...  
```
### patch
```cpp
  friend class BraveContentsContainerView;
  virtual void UpdateBorderAndOverlay(bool is_in_split,

```

### match
```cpp
...
>>>
 void UpdateBorderRoundedCorners(); 
<<< 
...
```
### patch
```cpp
  virtual void UpdateBorderRoundedCorners();

```

