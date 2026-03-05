### match
```
...
 # ifndef ... 
 namespace blink { ... 
 std::unique_ptr<WebPrescientNetworking> prescient_networking 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```
  void CopyImageAtViewportPoint_UnUsed() {}
  SkBitmap GetImageAtViewportPoint(const gfx::Point& viewport_point);

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
static BlockingDetailsList ConvertFeatureAndLocationToMojomStruct(
      const BFCacheBlockingFeatureAndLocations&,
      const BFCacheBlockingFeatureAndLocations&);  >>> 
 bool IsSameOrigin();  <<< ... 
v8_compile_hints::V8LocalCompileHintsProducer&
  GetV8LocalCompileHintsProducer() {
    return *v8_local_compile_hints_producer_;
  }
 ... } ...  
```
### patch
```
  bool IsSameOrigin(__VA_ARGS__); 
  url::Origin origin_for_clear_window_name_check_;

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
// Can only be called while the frame is not detached.  >>> 
 bool ScriptEnabled();  <<< ... 
const WebPrintParams& GetPrintParams() const;
 ... } ...  
```
### patch
```
  bool ScriptEnabled(const KURL& script_url);
  bool ScriptEnabled_ChromiumImpl();

```

