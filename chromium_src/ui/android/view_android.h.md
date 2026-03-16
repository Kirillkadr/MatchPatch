### match
```cpp

...
 # ifndef ... 
 namespace ui { ... 
 class UI_ANDROID_EXPORT ViewAndroid { ... 
friend class WindowAndroid;  >>> 
 bool OnDragEvent(const DragEventAndroid& event);  <<< ... 
bool OnTouchEvent(const MotionEventAndroid& event);
 ... } ...  } ...  
```
### patch
```cpp

  Unused() {
    return false;
  }
  friend class speedreader::SpeedreaderTabHelper;
  bool OnDragEvent

```

### match
```cpp

...
 # ifndef ... 
 namespace ui { ... 
;
 } 
 // namespace ui 
 >>> 
 ... 
```
### patch
```cpp

namespace speedreader {
class SpeedreaderTabHelper;
}

```

