### match
```cpp
...
 
 # ifndef ... 
#include "base/memory/weak_ptr.h"

 #include "base/observer_list.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/profiles/brave_profile_avatar_downloader.h"

```

### match
```cpp
...
 
 # ifndef ...   >>> 
 class ProfileAvatarDownloader 
 ;  <<< 
class PrefRegistrySimple
 ... 
```
### patch
```cpp
class BraveProfileAvatarDownloader;

```

