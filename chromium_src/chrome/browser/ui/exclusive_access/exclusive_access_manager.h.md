### match
```cpp
...
 
 # ifndef ... 
 
 class ExclusiveAccessManager { ... 
 
 FullscreenController* fullscreen_controller() { ... 
return &fullscreen_controller_;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
  const FullscreenController* fullscreen_controller() const {
    return &fullscreen_controller_;
  }

```

