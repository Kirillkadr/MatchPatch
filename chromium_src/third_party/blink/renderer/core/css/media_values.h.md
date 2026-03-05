### match
```
...
 # ifndef ... 
 namespace blink { ... 
static float CalculateLineHeight(LocalFrame*);  >>> 
 static int CalculateDeviceWidth(LocalFrame*); 
 static int CalculateDeviceHeight(LocalFrame*);  <<< ... 
static bool CalculateStrictMode(LocalFrame*);
 ... } ...  
```
### patch
```
  static int CalculateDeviceWidth(LocalFrame*, bool);
  static int CalculateDeviceWidth_ChromiumImpl(LocalFrame*);

  static int CalculateDeviceHeight(LocalFrame*, bool);
  static int CalculateDeviceHeight_ChromiumImpl(LocalFrame*);

```

