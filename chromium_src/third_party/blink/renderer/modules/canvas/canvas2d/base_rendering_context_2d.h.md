### match
```
...
>>>
 virtual 
 ImageData 
 * 
 getImageDataInternal 
 ( 
 int sx 
 ,  <<< ... 
int sy
 ... ) ...  
```
### patch
```
  virtual ImageData* getImageDataInternal(ScriptState*, int sx, int sy, int sw, int sh,
                       ImageDataSettings*, ExceptionState&);
  ImageData* getImageDataInternal(int sx, int sy, int sw, int sh,
                                  ImageDataSettings*, ExceptionState&);
  ImageData* getImageData(ScriptState*, int sx, int sy, int sw, int sh,
                          ExceptionState&);
  ImageData* getImageData(ScriptState*, int sx, int sy, int sw, int sh,
                          ImageDataSettings*, ExceptionState&);
  ImageData* getImageData_Unused(int sx, int sy, int sw, int sh,
                                 ExceptionState&);
  ImageData* getImageData_Unused(int sx, int sy, int sw, int sh,
                                 ImageDataSettings*, ExceptionState&);         
  virtual ImageData* getImageDataInternal_Unused(int sx,

```

