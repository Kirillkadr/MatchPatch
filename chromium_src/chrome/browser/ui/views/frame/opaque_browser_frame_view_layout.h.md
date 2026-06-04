### match
```cpp
...
 
 class OpaqueBrowserFrameViewLayout : public views::LayoutManager { ... 
>>> 
 void 
 SetBoundsForButton 
 ( 
 views::FrameButton button_id 
 , 
<<< 
...) ...  } ...  
```
### patch
```cpp
  friend class BrowserFrameViewLayoutLinux;
  virtual void SetBoundsForButton(views::FrameButton button_id,

```

