### match
```cpp
...
 #include <vector>
 
 >>> 
 ...
```
### patch
```cpp
#include "components/translate/core/browser/translate_prefs.h"
#include <string_view>

#include "brave/components/translate/core/common/brave_translate_features.h"

```

### match
```cpp
...
 
  std::string_view base_language = language::ExtractBaseLanguage(language_code);
  for (const auto& item : list) {
    if (base_language == language::ExtractBaseLanguage(item))
      return true;
  }
  return false;

 } 
 >>> 
 ...
```
### patch
```cpp
#define TranslatePrefs TranslatePrefs_ChromiumImpl

```

### match
```cpp
...
 
 namespace translate { ... 
 
 bool TranslatePrefs::IsDictionaryEmpty(const char* pref_id) const { ... 
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
#undef TranslatePrefs
bool TranslatePrefs::ShouldAutoTranslate(std::string_view source_language,
                                         std::string* target_language) {
  if (!IsBraveAutoTranslateEnabled()) {
    return false;
  }

  return TranslatePrefs_ChromiumImpl::ShouldAutoTranslate(source_language,
                                                          target_language);
}

```

