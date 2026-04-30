### match
```cpp
...
 
 namespace features { ... 
 
 BASE_FEATURE ( ... 
kPrefetchOffTheMainThread,
             
 base::FEATURE_DISABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kPrefetchClientHints, base::FEATURE_DISABLED_BY_DEFAULT},
    {kPrefetchScheduler, base::FEATURE_DISABLED_BY_DEFAULT},
    {kPrefetchServiceWorker, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

