### match
```
...
#include "ui/base/resource/scoped_startup_resource_bundle.h"

 #include "ui/base/ui_base_switches.h"
 
 >>> 
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_CHROMEOS) || \
    BUILDFLAG(IS_MAC)
#include "components/webapps/isolated_web_apps/scheme.h"
#endif
 ... 
```
### patch
```
#include "brave/app/brave_main_delegate.cc"  // IWYU pragma: export

```

