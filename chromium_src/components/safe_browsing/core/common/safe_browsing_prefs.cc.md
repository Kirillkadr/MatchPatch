### match
```cpp
...
 
 namespace safe_browsing { ... 
 bool 
 IsEnhancedProtectionEnabled(const PrefService& prefs) 
 { 
 >>> 
// SafeBrowsingEnabled is checked too due to devices being out
 ... } ...  } ...  
```
### patch
```cpp
  return false;

```

