### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class PLATFORM_EXPORT ImageDataBuffer { ... 
 const double& quality 
 ) 
 const 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```
  bool EncodeImage_Unused();        
  SkPixmap pixmap_multable() {
    return pixmap_;
  }

```

