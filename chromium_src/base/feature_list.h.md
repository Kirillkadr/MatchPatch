### match
```
...
 # ifndef ... 
 namespace base { ... 
 class BASE_EXPORT FeatureList { ... 
// reason (e.g. command line or field trial). Note: This will return true even
 // when a feature is overridden with OVERRIDE_USE_DEFAULT (default group). 
 >>> 
bool IsFeatureOverridden(std::string_view feature_name) const;
 ... } ...  } ...  
```
### patch
```
  bool  IsFeatureOverridden_ChromiumImpl(std::string_view feature_name) const;
  static FeatureState GetCompileTimeFeatureState(const Feature& feature);

```

### match
```
...
 # ifndef ... 
 namespace base { ... 
 class BASE_EXPORT FeatureList { ... 
// name must only have a single corresponding Feature struct, which is checked
 // in builds with DCHECKs enabled. 
 >>> 
static std::optional<bool> GetStateIfOverridden(const Feature& feature);
 ... } ...  } ...  
```
### patch
```
  static std::optional<bool> GetStateIfOverridden_ChromiumImpl(const Feature& feature); 

```

