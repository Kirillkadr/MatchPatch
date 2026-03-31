### match
```cpp
...
#include "components/signin/public/base/signin_pref_names.h"

 #include "google_apis/google_api_keys.h"
 
 >>> 
#if BUILDFLAG(IS_CHROMEOS)
#include "chrome/browser/ash/account_manager/account_manager_util.h"
#endif
 ... 
```
### patch
```cpp
#if BUILDFLAG(IS_ANDROID)
#define BRAVE_COMPUTE_ACCOUNT_CONSISTENCY_METHOD \
  return AccountConsistencyMethod::kDisabled;
#else
#define BRAVE_COMPUTE_ACCOUNT_CONSISTENCY_METHOD
#endif


```

