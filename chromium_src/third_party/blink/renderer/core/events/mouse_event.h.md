### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT MouseEvent : public UIEventWithKeyState { ... 
// values exposed via DOM APIs are invariant under zooming.  >>> 
 virtual double screenX() const { return std::floor(screen_x_); } 
 virtual double screenY() const { return std::floor(screen_y_); }  <<< ... 
virtual double clientX() const { return std::floor(client_x_); }
 ... } ...  } ...  
```
### patch
```
  virtual double screenX() const {
    return brave::FarbledPointerScreenCoordinate(
        view(), brave::FarbleKey::kPointerScreenX, clientX(),
        screenX_ChromiumImpl());
  }
  virtual double screenX_ChromiumImpl() const { return std::floor(screen_x_); }
  virtual double screenY() const {
    return brave::FarbledPointerScreenCoordinate(
        view(), brave::FarbleKey::kPointerScreenY, clientY(),
        screenY_ChromiumImpl());
  }
  virtual double screenY_ChromiumImpl() const { return std::floor(screen_y_); }

```

