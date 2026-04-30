### match
```cpp
...
#include "base/supports_user_data.h"

 #include "base/version.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/startup/brave_startup_tab_provider_impl.h"

```

### match
```cpp
...
>>>
 StartupTabProviderImpl() 
 , 
 process_startup 
 , 
 is_incognito_or_guest 
 ,  <<<  ...
```
### patch
```cpp
      BraveStartupTabProviderImpl(), process_startup, is_incognito_or_guest,

```

