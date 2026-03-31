### match
```cpp
...
 
 # ifndef ... 
 
 namespace extensions { ... 
// See also: GetManifestHomePageURL(), SpecifiedHomepageURL()  >>> 
 static GURL GetHomepageURL(const Extension* extension);  <<< 
// Returns true if the extension specified a valid home page url in the
 ... } ...  
```
### patch
```cpp
  static GURL GetHomepageURL_Unused(const Extension* extension);
  static const GURL GetHomepageURL(const Extension* extension);


```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace extensions { ... 
// See also: GetHomepageURL()  >>> 
 static GURL GetWebStoreURL(const Extension* extension);  <<< 
// Returns the Update URL for this extension.
 ... } ...  
```
### patch
```cpp
  static GURL GetWebStoreURL_ChromiumImpl(const Extension* extension); 
  static const GURL GetWebStoreURL(const Extension* extension);

```

