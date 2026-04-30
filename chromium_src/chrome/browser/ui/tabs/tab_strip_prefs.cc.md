### match
```cpp
...
 
 namespace tabs { ... 
 bool 
 GetDefaultTabSearchRightAligned() 
 { 
 >>> 
// These platforms are all left aligned, the others should be right.
 ... } ...  } ...  
```
### patch
```cpp
return true;

```

