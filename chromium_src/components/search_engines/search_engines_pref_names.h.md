### match
```cpp
...
 #define COMPONENTS_SEARCH_ENGINES_SEARCH_ENGINES_PREF_NAMES_H_
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/search_engines/brave_search_engines_pref_names.h"

```

### match
```cpp
...
 
 namespace prefs { ... 
inline constexpr char kDefaultSearchProviderChoiceScreenSkippedCount[] =
    "default_search_provider.skip_count";
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
inline constexpr char kDefaultSearchProviderByExtension[] =
    "brave.default_search_provider_by_extension";
inline constexpr char kBraveDefaultSearchVersion[] =
    "brave.search.default_version";
inline constexpr char kSyncedDefaultPrivateSearchProviderGUID[] =
    "brave.default_private_search_provider_guid";
inline constexpr char kSyncedDefaultPrivateSearchProviderData[] =
    "brave.default_private_search_provider_data";

```

