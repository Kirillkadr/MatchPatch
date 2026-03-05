### match
```
...
 # ifndef ... 
 namespace blink { ... 
void Trace(Visitor*) const override;  >>> 
 ImageData* getImageDataInternal(int sx,
                                  int sy,
                                  int sw,
                                  int sh,
                                  ImageDataSettings*,
                                  ExceptionState&) final;  <<< ... 
void SendContextLostEventIfNeeded() override;
 ... } ...  
```
### patch
```
  ImageData* getImageDataInternal(ScriptState*, int sx, int sy, int sw, int sh, \
                       ImageDataSettings*, ExceptionState&) final;   \

```

