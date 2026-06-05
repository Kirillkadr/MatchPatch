### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/regional_capabilities/regional_capabilities_service.h"

 ... 
```
### patch
```cpp
#include "components/regional_capabilities/regional_capabilities_service.h"

```

### match
```cpp
...
#include "components/regional_capabilities/regional_capabilities_service.h"

 #include "components/regional_capabilities/regional_capabilities_service.h"
 
 >>> 
#include <algorithm>

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
 
 Program CountryIdToProgramForTesting(
    const country_codes::CountryId& country_id) { ... 
return CountryIdToProgram(country_id);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
TemplateURLPrepopulateData::BravePrepopulatedEngineID
RegionalCapabilitiesService::GetRegionalDefaultEngine() {
  return GetDefaultEngine(GetCountryIdInternal(), profile_prefs_.get());
}

```

