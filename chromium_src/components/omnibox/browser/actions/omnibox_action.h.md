### match
```cpp
...
 
 # ifndef ... 
#define COMPONENTS_OMNIBOX_BROWSER_ACTIONS_OMNIBOX_ACTION_H_

 #include <string>
 
 >>> 
#include "base/functional/callback.h"

 ... 
```
### patch
```cpp
#include "brave/components/ai_chat/core/common/buildflags/buildflags.h"
#include "brave/components/commander/common/buildflags/buildflags.h"
#if BUILDFLAG(ENABLE_COMMANDER)
#include "brave/components/commander/browser/commander_frontend_delegate.h"
#endif  // BUILDFLAG(ENABLE_COMMANDER)

```

### match
```cpp
...
 
 # ifndef ... 
// were clicked.
 virtual void OpenSharingHub() = 0; 
 >>> 
// Opens and shows a new incognito browser window.
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_COMMANDER)
    virtual void OpenSharingHub() = 0;
    virtual commander::CommanderFrontendDelegate* GetCommanderDelegate() = 0;
#endif  // BUILDFLAG(ENABLE_COMMANDER)


```

### match
```cpp
...
 
 # ifndef ... 
// Opens and shows a new incognito browser window.
 virtual void NewIncognitoWindow() = 0; 
 >>> 
// Opens an Incognito clear browsing data dialog.
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_AI_CHAT)
    virtual void NewIncognitoWindow() = 0;
    virtual void OpenLeo(const std::u16string& query) = 0;
    virtual bool IsLeoProviderEnabled() = 0;
#endif

```

