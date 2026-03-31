### match
```cpp
...
 
 # ifndef ... 
 #define GOOGLE_APIS_GOOGLE_API_KEYS_H_
 
 >>> 
#include <string>

 ... 
```
### patch
```cpp
#include <string>

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace google_apis { ... 
base::ScopedClosureRunner
 SetScopedApiKeyCacheForTesting(ApiKeyCache* api_key_cache) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
COMPONENT_EXPORT(GOOGLE_APIS)
void SetAPIKeyForTesting(const std::string& api_key);

COMPONENT_EXPORT(GOOGLE_APIS)
bool BraveHasAPIKeyConfigured();

```

