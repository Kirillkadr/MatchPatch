### match
```
...
// experiment, bug, the deletion of a file, etc.
 #include "media/base/media_switches.h"
 
 >>> 
#include "base/command_line.h"

 ... 
```
### patch
```
#include "base/feature_override.h"

```

### match
```
...
 
 namespace media { ...  >>>  } ...  
```
### patch
```
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kLiveCaption, base::FEATURE_DISABLED_BY_DEFAULT},
    {kEnableTabMuting, base::FEATURE_ENABLED_BY_DEFAULT},
}});

```

