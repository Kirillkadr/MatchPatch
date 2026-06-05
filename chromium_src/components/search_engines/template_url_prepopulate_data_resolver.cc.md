### match
```cpp
...
#include "components/search_engines/template_url_prepopulate_data_resolver.h"

 #include <optional>
 
 >>> 
#include "base/logging.h"

 ... 
```
### patch
```cpp
#include "components/search_engines/template_url_prepopulate_data.h"

```

### match
```cpp
...
 
 namespace TemplateURLPrepopulateData { ... 
 
 std::unique_ptr<TemplateURLData> Resolver::GetFallbackSearch() const { ... 
>>> 
 return 
 TemplateURLPrepopulateData::GetPrepopulatedFallbackSearch 
 ( 
<<< 
profile_prefs_.get()
 ... ) ...  } ...  } ...  
```
### patch
```cpp
  return TemplateURLPrepopulateData::GetPrepopulatedFallbackSearch(regional_capabilities_->GetRegionalDefaultEngine(),

```

