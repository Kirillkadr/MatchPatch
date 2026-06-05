### match
```cpp
...
#include <memory>

 #include <utility>
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```cpp
#include "base/check_is_test.h"
#include "build/build_config.h"
#include "components/prefs/pref_service.h"
#include "components/search_engines/search_engines_pref_names.h"

```

### match
```cpp
...
#include "base/enterprise_util.h"

 #endif 
 // BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC) 
 >>> 
namespace {
bool g_fallback_search_engines_disabled = false;
}
 ... 
```
### patch
```cpp
namespace {
bool IsDefaultSearchProviderByExtension(PrefService* pref_service) {
  // |kDefaultSearchProviderByExtension| is only used by desktop.
#if BUILDFLAG(IS_ANDROID)
  return false;
#else
  if (pref_service->FindPreference(prefs::kDefaultSearchProviderByExtension)) {
    return pref_service->GetBoolean(prefs::kDefaultSearchProviderByExtension);
  } else {
    CHECK_IS_TEST();
    return false;
  }
#endif
}

}  // namespace

```

### match
```cpp
...
 
 void DefaultSearchManager::LoadDefaultSearchEngineFromPrefs() { ... 
 
 if (pref->IsExtensionControlled()) { ... 
 extension_default_search_ = std::move(turl_data); 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
    } else if (IsDefaultSearchProviderByExtension(pref_service_))  {  
    extension_default_search_ = std::move(turl_data);
// clang-format on

```

