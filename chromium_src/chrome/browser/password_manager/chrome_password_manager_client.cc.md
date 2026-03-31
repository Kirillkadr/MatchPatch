### match
```cpp
...
#include "base/types/expected.h"

 #include "base/types/optional_util.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/constants/pref_names.h"

```

### match
```cpp
...
 
 bool ChromePasswordManagerClient::IsFillingEnabled(const GURL& url) const { ...   >>> 
 if 
 (!profile || profile->IsGuestSession()) 
 {  <<< 
return false;
 ... } ...  } ...  
```
### patch
```cpp
  if (!profile || profile->IsGuestSession() ||                                                    
      (!profile->GetPrefs()->GetBoolean(kBraveAutofillPrivateWindows) &&
       (IsOffTheRecord() || profile->IsTor())) ||
      profile->IsGuestSession()) {

```

