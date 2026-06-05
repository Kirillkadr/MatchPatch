### match
```cpp
...
 
 namespace remote_cocoa { ... 
void OnWindowWillClose();
 // Called by the NSWindowDelegate when the size of the window changes. 
 >>> 
void OnSizeChanged();
 ... } ...  
```
### patch
```cpp
  void SetWindowTitleVisibility(bool visible) override;
  void ResetWindowControlsPosition() override;
  void UpdateWindowTitleColor(SkColor color) override;

```

