### match
```cpp
...
 #include <stddef.h>
 
 >>> 
 ...
```
### patch
```cpp
#include <string_view>

```

### match
```cpp
...
 #include "components/prefs/scoped_user_pref_update.h"
 
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
 static bool force_translate_on_english_for_testing_;
 >>> 
 ...
```
### patch
```cpp
#undef TranslatePrefs

```

### match
```cpp
...
 
 namespace translate { ... 
 >>> 
  } ...
```
### patch
```cpp
class TranslatePrefs : public TranslatePrefs_ChromiumImpl {
 public:
  using TranslatePrefs_ChromiumImpl::TranslatePrefs_ChromiumImpl;
  // Override to control by Brave features. No virtual because TranslatePrefs
  // doesn't have a virtual dtor and the method isn't used inside the impl.
  bool ShouldAutoTranslate(std::string_view source_language,
                           std::string* target_language);
};

```

