### match
```
...
 # ifndef ... 
 namespace blink { ... 
 public 
 : 
 >>> 
static bool supports(const AtomicString&);
 ... } ...  
```
### patch
```
  static bool supports_ChromiumImpl(const AtomicString&); 

```

