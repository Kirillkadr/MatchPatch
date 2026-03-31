### match
```cpp
...
#include "chrome/browser/prefs/pref_service_incognito_allowlist.h"

 #include <vector>
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/prefs/brave_pref_service_incognito_allowlist.h"

```

### match
```cpp
...
 
 namespace { ...   >>> 
 bookmarks::prefs::kShowBookmarkBar 
 ,  <<< 
#if BUILDFLAG(IS_ANDROID)
 ... } ...  
```
### patch
```cpp
    bookmarks::prefs::kShowBookmarkBar, bookmarks::prefs::kAlwaysShowBookmarkBarOnNTP,

```

### match
```cpp
...
 
 namespace prefs { ...   >>> 
 std::vector<const char*> 
 GetIncognitoPersistentPrefsAllowlist() 
 {  <<< 
std::vector<const char*> allowlist;
 ... } ...  } ...  
```
### patch
```cpp
std::vector<const char*> GetIncognitoPersistentPrefsAllowlist_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace prefs { ... 
 
 std::vector<const char*> GetIncognitoPersistentPrefsAllowlist_ChromiumImpl() { ... 
return allowlist;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
std::vector<const char*> GetIncognitoPersistentPrefsAllowlist() {
  std::vector<const char*> allowlist =
      GetIncognitoPersistentPrefsAllowlist_ChromiumImpl();
  for (auto pref : brave::GetBravePersistentPrefNames()) {
    allowlist.push_back(pref.data());
  }
  return allowlist;
}


```

