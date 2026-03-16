### match
```
...
#include "base/strings/stringprintf.h"

 #include "base/strings/sys_string_conversions.h"
 
 >>> 
#import "chrome/browser/mac/dock.h"

 ... 
```
### patch
```
#include "brave/browser/mac/keystone_glue.h"

```

### match
```
...
 
 bool MaybeInstallFromDiskImage() { ... 
 
 if (!InstallFromDiskImage(std::move(authorization), installer_url,
                              source_path, target_path)) { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```
    dock::ChromeIsInTheDock();
  KeystoneGlue* keystone_glue = [KeystoneGlue defaultKeystoneGlue];
  [keystone_glue setAppPath:target_path];
  [keystone_glue promoteTicketWithAuthorization:std::move(authorization)
                                    synchronous:YES];                    

```

