### match
```
...
 # ifndef ... 
 namespace blink { ... 
 static const char kSupplementName[]; 
 >>> 
static Keyboard* keyboard(Navigator&);
 ... } ...  
```
### patch
```
  static Keyboard* keyboard_ChromiumImpl(Navigator&); 

```

