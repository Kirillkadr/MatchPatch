### match
```
...
 # ifndef ... 
#include "base/memory/weak_ptr.h"

 #include "build/build_config.h"
 
 >>> 
#include "chrome/browser/autocomplete/chrome_autocomplete_scheme_classifier.h"

 ... 
```
### patch
```
#include "brave/components/ai_chat/core/common/buildflags/buildflags.h"
#include "brave/components/commander/common/buildflags/buildflags.h"

```

### match
```
...
#else
#include "chrome/browser/autocomplete/tab_matcher_desktop.h"

 #endif 
 >>> 
 ... 
```
### patch
```
#if BUILDFLAG(ENABLE_COMMANDER)
#include "brave/components/commander/browser/commander_frontend_delegate.h"
#define GetAutocompleteClassifier       \
  GetAutocompleteClassifier() override; \
  commander::CommanderFrontendDelegate* GetCommanderDelegate
#endif  // BUILDFLAG(ENABLE_COMMANDER)

#if BUILDFLAG(ENABLE_AI_CHAT)
#define GetInMemoryDatabase                           \
  GetInMemoryDatabase() override;                     \
  void OpenLeo(const std::u16string& query) override; \
  bool IsLeoProviderEnabled
#endif


```

### match
```
...
 #endif 
 // CHROME_BROWSER_AUTOCOMPLETE_CHROME_AUTOCOMPLETE_PROVIDER_CLIENT_H_ 
 >>> 
 ... 
```
### patch
```

#if BUILDFLAG(ENABLE_AI_CHAT)
#undef GetInMemoryDatabase
#endif
```

