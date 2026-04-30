### match
```cpp
...
 
 # ifndef ... 
 
 namespace history { ... 
// How many top sites to store in the cache.  >>> 
 static constexpr size_t kTopSitesNumber = 10;  <<<  ...} ...  
```
### patch
```cpp
static constexpr size_t kTopSitesNumber = 12; 
  static constexpr size_t kTopSitesNumber_Unused = 10;

```

