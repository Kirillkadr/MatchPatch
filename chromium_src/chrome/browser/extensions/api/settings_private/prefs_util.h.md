### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ... 
// manipulate.  >>> 
 const TypedPrefMap& GetAllowlistedKeys();  <<< 
// Returns the pref type for |pref_name| or PREF_TYPE_NONE if not in the
 ... } ...  
```
### patch
```
  virtual const TypedPrefMap& GetAllowlistedKeys();

```

