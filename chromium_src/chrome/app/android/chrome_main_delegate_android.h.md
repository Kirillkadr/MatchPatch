### match
```
...
 # ifndef ... 
#include <variant>

 #include "chrome/app/chrome_main_delegate.h"
 
 >>> 
#include "components/safe_browsing/buildflags.h"

 ... 
```
### patch
```
#include "brave/app/brave_main_delegate.h"

```

### match
```
...
 # ifndef ...   >>> 
 class 
 ChromeMainDelegateAndroid 
 : public ChromeMainDelegate 
 {  <<< ... 
public
 ... } ...  
```
### patch
```
class ChromeMainDelegateAndroid : public BraveMainDelegate {

```

