### match
```cpp
...
>>>
 bool ControlsHitTestContainsPoint(const gfx::Point& point); 
<<< 
...
```
### patch
```cpp
  bool virtual ControlsHitTestContainsPoint(const gfx::Point& point);

```

### match
```cpp
...
// Called when the bounds of the controls should be updated.
>>> 
 void OnUpdateControlsBounds(); 
<<< 
...
```
### patch
```cpp
  void virtual OnUpdateControlsBounds();

```

### match
```cpp
...
// Set up the views::Views that will be shown on the window.
>>> 
 void SetUpViews(); 
<<< 
// Finish initialization by performing the steps that require the root View.
 ... 
```
### patch
```cpp
  friend class BraveVideoOverlayWindowViews;
  virtual void SetUpViews();

```

### match
```cpp
...
//    * The origin URL has high media engagement or is a file
>>> 
 bool IsTrustedForMediaPlayback() const; 
<<< 
// Updates the value of `meets_user_interaction_` if needed.
 ... 
```
### patch
```cpp
  bool virtual IsTrustedForMediaPlayback() const;

```

