### match
```
...
 # ifndef ... 
 namespace blink { ... 
double clientY() const { return client_pos_.y(); }  >>> 
 double screenX() const { return screen_pos_.x(); } 
 double screenY() const { return screen_pos_.y(); }  <<< ... 
double pageX() const { return page_pos_.x(); }
 ... } ...  
```
### patch
```
  double screenX() const {
    return brave::FarbledPointerScreenCoordinate(
        target()->ToDOMWindow(), brave::FarbleKey::kPointerScreenX, clientX(),
        screenX_ChromiumImpl());
  }
  double screenX_ChromiumImpl() const { return screen_pos_.x(); }
  double screenY() const {
    return brave::FarbledPointerScreenCoordinate(
        target()->ToDOMWindow(), brave::FarbleKey::kPointerScreenY, clientY(),
        screenY_ChromiumImpl());
  }
  double screenY_ChromiumImpl() const { return screen_pos_.y(); }

```

