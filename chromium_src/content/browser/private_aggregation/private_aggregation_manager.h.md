### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class CONTENT_EXPORT PrivateAggregationManager { ... 
 virtual 
 ~PrivateAggregationManager() = default; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  static PrivateAggregationManager* GetManager_ChromiumImpl(BrowserContext& browser_context); 

```

