### match
```cpp
...
 #define CHROME_BROWSER_UI_VIEWS_OVERLAY_SIMPLE_OVERLAY_WINDOW_IMAGE_BUTTON_H_
 
 >>> 
 ... 
```
### patch
```cpp
#include <optional>

```

### match
```cpp
...
 private 
 : 
 >>> 
 ... 
```
### patch
```cpp
  void override_icon(const gfx::VectorIcon& icon) {
    *const_cast<raw_ref<const gfx::VectorIcon>*>(&icon_) = icon;
  }
  void set_icon_size(int size) {
    icon_size_ = size;
  }
  friend class BraveVideoOverlayWindowViews;
  std::optional<int> icon_size_;

```

