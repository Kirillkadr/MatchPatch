### match
```cpp
...
// found in the LICENSE file.
 #include "components/password_manager/core/browser/features/password_features.h"
 
 >>> 
#include "base/feature_list.h"

 ...
```
### patch
```cpp
#include "base/feature_override.h"
#include "build/build_config.h"

```

### match
```cpp
...
  BASE_FEATURE(kWebAuthnUsePasskeyFromAnotherDeviceInContextMenu,
             base::FEATURE_ENABLED_BY_DEFAULT);

#endif  // !BUILDFLAG(IS_ANDROID) && !BUILDFLAG(IS_IOS)
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
#if BUILDFLAG(IS_IOS) || BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_MAC) || \
    BUILDFLAG(IS_WIN)
    {kSkipUndecryptablePasswords, base::FEATURE_ENABLED_BY_DEFAULT},
#endif
}});

```

