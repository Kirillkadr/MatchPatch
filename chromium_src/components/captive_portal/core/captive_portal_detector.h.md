### match
```cpp
...
 
 # ifndef ... 
 
 namespace captive_portal { ... 
 
 class CAPTIVE_PORTAL_EXPORT CaptivePortalDetector { ... 
// for this URL.
 static const std::string_view GetDefaultUrl(); 
 >>> 
explicit CaptivePortalDetector(
      network::mojom::URLLoaderFactory* loader_factory);

  CaptivePortalDetector(const CaptivePortalDetector&) = delete;
 ... } ...  } ...  
```
### patch
```cpp
  static const std::string_view GetDefaultUrl_ChromiumImpl
();

```

