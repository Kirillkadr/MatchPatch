### match
```
...
#include <utility>

 #include "base/values.h"
 
 >>> 
#include "chrome/browser/browser_process.h"

 ... 
```
### patch
```
#include "brave/browser/extensions/api/settings_private/brave_prefs_util.h"

```

### match
```
...
 
 namespace extensions { ... 
 
 SettingsPrivateDelegate::SettingsPrivateDelegate(Profile* profile)
    : profile_(profile) { ...   >>> 
 prefs_util_ = std::make_unique<PrefsUtil>(profile);  <<<  ...} ...  } ...  
```
### patch
```
  prefs_util_ = std::make_unique<BravePrefsUtil>(profile);

```

