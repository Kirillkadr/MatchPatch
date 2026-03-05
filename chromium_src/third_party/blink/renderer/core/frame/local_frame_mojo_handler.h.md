### match
```
...
 # ifndef ... 
 namespace blink { ... 
void Focus() final;
 void ClearFocusedElement() final; 
 >>> 
void CopyImageAt(const gfx::Point& window_point) final;
 ... } ...  
```
### patch
```
  void GetImageAt(const gfx::Point& window_point, GetImageAtCallback callback) 
      final;

```

