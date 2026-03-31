### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 class CONTENT_EXPORT BrowsingDataFilterBuilder { ... 
// contexts, but anything embedded on it is left untouched.  >>> 
 kOriginInAllContexts 
 ,  <<< 
// Third option: StorageKeys are matched on both origin and top-level-site.
 ... } ...  } ...  
```
### patch
```cpp
    kOriginInAllContexts, kThirdPartiesOnly,

```

