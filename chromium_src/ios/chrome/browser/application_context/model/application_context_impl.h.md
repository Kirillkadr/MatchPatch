### match
```
...
 
 # ifndef ... 
// that requres all threads running.  >>> 
 void PreMainMessageLoopRun();  <<< 
// Most cleanup is done by these functions, driven from IOSChromeMainParts
 ... 
```
### patch
```
  // Makes PreMainMessageLoopRun virtual so that we can override it in
// BraveApplicationContextImpl
  void virtual PreMainMessageLoopRun();

```

