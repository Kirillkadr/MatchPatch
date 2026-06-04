### match
```cpp
...
 
 # ifndef ... 
 
 class COMPONENTS_PREFS_EXPORT PrefService { ... 
// specified, it will return the specified value.  Otherwise, the default
 // value (set when the pref was registered) will be returned. 
 >>> 
bool GetBoolean(std::string_view path) const;
 ... } ...  
```
### patch
```cpp
  bool GetBooleanOr(const std::string& path, bool other) const; 

```

