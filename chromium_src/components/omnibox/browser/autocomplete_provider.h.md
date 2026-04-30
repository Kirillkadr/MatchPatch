### match
```cpp
...
 
 # ifndef ... 
 
 class AutocompleteProvider
    : public base::RefCountedThreadSafe<AutocompleteProvider> { ...   >>> 
 TYPE_BOOKMARK = 1 << 0 
 ,  <<< 
TYPE_BUILTIN = 1 << 1
 ... } ...  
```
### patch
```cpp
    TYPE_BRAVE_COMMANDER = -1 << 0, TYPE_BRAVE_LEO = -1 << 1, TYPE_BOOKMARK = 1 << 0,

```

