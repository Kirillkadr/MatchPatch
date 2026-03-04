### match
```
...
 
 # ifndef ... 
const char* GetNameForLogging() override;
 static void MaybeCreateAndAdd(content::NavigationThrottleRegistry& registry); 
 >>> 
// The throttle normally ignores testing profiles and returns PROCEED. This
 ... 
```
### patch
```
  static void MaybeCreateAndAdd_ChromiumImpl(content::NavigationThrottleRegistry& registry);

```

