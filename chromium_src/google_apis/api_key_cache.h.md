### match
```cpp
...
 namespace google_apis { ... 
 class COMPONENT_EXPORT(GOOGLE_APIS) ApiKeyCache { ... 
const std::string& api_key_cros_chrome_geo() const {
    return api_key_cros_chrome_geo_;
  }
 #endif 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void set_api_key_for_testing(const std::string& api_key) {
    api_key_ = api_key;
  }

```

