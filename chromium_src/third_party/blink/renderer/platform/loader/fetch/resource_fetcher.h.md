### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class PLATFORM_EXPORT ResourceFetcher
    : public GarbageCollected<ResourceFetcher> { ... 
Resource*,
                          base::TimeTicks finish_time,
                          LoaderFinishType,
                          
 uint32_t inflight_keepalive_bytes 
 ) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```

  String GetContextCacheIdentifier() const; 

```

