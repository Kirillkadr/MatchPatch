### match
```cpp
...
 
 # ifndef ... 
 
 namespace optimization_guide { ... 
 PrefService* pref_service 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
bool IsUserPermittedToFetchFromRemoteOptimizationGuide(
    bool is_off_the_record,
    PrefService* pref_service) {
  return false;
}

```

