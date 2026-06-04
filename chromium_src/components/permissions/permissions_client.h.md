### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 
 class PermissionsClient { ... 
// origin checks for the passed in origins. Less strict ID checks than
 // `GetCanonicalOriginOverride`. 
 >>> 
virtual bool CanBypassEmbeddingOriginCheck(const GURL& requesting_origin,
                                             const GURL& embedding_origin);
 ... } ...  } ...  
```
### patch
```cpp
  virtual bool BraveCanBypassEmbeddingOriginCheck(const GURL& requesting_origin, 
                                     const GURL& embedding_origin,
                                     ContentSettingsType type);

```

