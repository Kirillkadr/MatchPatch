### match
```cpp
...
 
"LinearHistogram::kBucketCount_MAX. Use a sparse histogram "
 "instead."); 
 >>>
```
### patch
```cpp
if (static_cast<intmax_t>(sample) >= 0)
```

