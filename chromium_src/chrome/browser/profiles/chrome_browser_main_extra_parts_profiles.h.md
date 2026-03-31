### match
```cpp
...
 
 # ifndef ... 
#include "chrome/browser/chrome_browser_main_extra_parts.h"
  >>> 
 class ChromeBrowserMainParts 
 ;  <<< 
void AddProfilesExtraParts(ChromeBrowserMainParts* main_parts);
 ... 
```
### patch
```cpp
class ChromeBrowserMainParts_ChromiumImpl;

```

### match
```cpp
...
 
 # ifndef ...   >>> 
 void AddProfilesExtraParts(ChromeBrowserMainParts* main_parts);  <<< 
class ChromeBrowserMainExtraPartsProfiles : public ChromeBrowserMainExtraParts {
 public:
  ChromeBrowserMainExtraPartsProfiles();
  ChromeBrowserMainExtraPartsProfiles(
      const ChromeBrowserMainExtraPartsProfiles&) = delete;
  ChromeBrowserMainExtraPartsProfiles& operator=(
      const ChromeBrowserMainExtraPartsProfiles&) = delete;
  ~ChromeBrowserMainExtraPartsProfiles() override;

  // Instantiates all chrome KeyedService factories, which is
  // especially important for services that should be created at profile
  // creation time as compared to lazily on first access.
  static void EnsureBrowserContextKeyedServiceFactoriesBuilt();

  // Overridden from ChromeBrowserMainExtraParts:
  void PreProfileInit() override;
}
 ... 
```
### patch
```cpp

void AddProfilesExtraParts(ChromeBrowserMainParts_ChromiumImpl* main_parts);

```

