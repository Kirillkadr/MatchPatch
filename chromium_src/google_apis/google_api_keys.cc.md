### match
```cpp
...
 
 namespace google_apis { ... 
 
 base::ScopedClosureRunner SetScopedApiKeyCacheForTesting(
    ApiKeyCache* api_key_cache) { ... 
return base::ScopedClosureRunner(base::BindOnce(
      [](ApiKeyCache* previous_value) {
        g_api_key_cache_instance = previous_value;
      },
      previous_value));
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void SetAPIKeyForTesting(const std::string& api_key) {
  GetApiKeyCacheInstance().set_api_key_for_testing(api_key);  // IN-TEST
}
bool BraveHasAPIKeyConfigured() {
  // Google API key is not used in brave for translation service, always return
  // true for the API key check so the flow won't be blocked because of missing
  // keys.
  return true;
}

```

