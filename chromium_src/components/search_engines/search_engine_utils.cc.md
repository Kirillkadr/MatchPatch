### match
```cpp
...
// found in the LICENSE file.
 #include "components/search_engines/search_engine_utils.h"
 
 >>> 
#include "base/not_fatal_until.h"

 ... 
```
### patch
```cpp
#include "base/compiler_specific.h"
#include "brave/components/search_engines/brave_prepopulated_engines.h"

```

### match
```cpp
...
 
 namespace search_engine_utils { ... 
>>> 
 SearchEngineType 
 GetEngineType(const GURL& url) 
 { 
<<< 
DCHECK(url.is_valid());
 ... } ...  } ...  
```
### patch
```cpp
SearchEngineType GetEngineType_ChromiumImpl(const GURL& url) {

```

### match
```cpp
...
 
 namespace search_engine_utils { ... 
 
 SearchEngineType GetEngineType_ChromiumImpl(const GURL& url) { ... 
return (*found_migrated_engine_it)->type;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
SearchEngineType GetEngineType(const GURL& url) {
  SearchEngineType type = GetEngineType_ChromiumImpl(url);
  if (type == SEARCH_ENGINE_OTHER) {
    for (const auto& entry : TemplateURLPrepopulateData::kBraveEngines) {
      const auto* engine = entry.second;
      if (SameDomain(url, GURL(engine->search_url))) {
        return engine->type;
      }
      for (const auto* alternate_url : engine->alternate_urls) {
        if (SameDomain(url, GURL(alternate_url))) {
          return engine->type;
        }
      }
    }
  }
  return type;
}

```

