### match
```cpp
...
#include <variant>

 #include <vector>
 
 >>> 
#include "base/auto_reset.h"

 ... 
```
### patch
```cpp
#include "brave/components/search_engines/brave_prepopulated_engines.h"

```

### match
```cpp
...
 
 namespace regional_capabilities { ... 
ScopedPrepopulatedEnginesOverride SetPrepopulatedEnginesOverrideForTesting(
    std::vector<const TemplateURLPrepopulateData::PrepopulatedEngine*>
        regional_engines,
    std::vector<const TemplateURLPrepopulateData::PrepopulatedEngine*>
        other_known_engines);
 void ClearPrepopulatedEnginesOverrideForTesting(); 
 >>> 
 ... } ...  
```
### patch
```cpp
TemplateURLPrepopulateData::BravePrepopulatedEngineID GetDefaultEngine(
    country_codes::CountryId country_id,
    PrefService& prefs);

```

