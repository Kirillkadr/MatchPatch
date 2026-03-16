### match
```
...
 
 # ifndef ... 
#include "base/scoped_observation.h"

 #include "base/time/time.h"
 
 >>> 
#include "build/chromeos_buildflags.h"

 ... 
```
### patch
```
#include "brave/browser/extensions/api/identity/brave_web_auth_flow.h"

```

### match
```
...
 
 # ifndef ... 
 
 namespace extensions { ...   >>> 
 class 
 IdentityGetAuthTokenFunction 
 : 
 public 
 ExtensionFunction 
 ,  <<< 
public
 ... } ...  
```
### patch
```
class IdentityGetAuthTokenFunction : public ExtensionFunction, public BraveWebAuthFlow,

```

