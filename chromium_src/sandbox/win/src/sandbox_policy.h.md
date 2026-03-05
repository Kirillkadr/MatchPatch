### match
```
...
 # ifndef ... 
 namespace sandbox { ... 
// this policy object.
 virtual bool IsConfigured() const = 0; 
 >>> 
// Sets the security level for the target process' two tokens.
 ... } ...  
```
### patch
```
  virtual void SetShouldPatchModuleFileName(bool) = 0; \
  virtual bool ShouldPatchModuleFileName() const = 0;

```

