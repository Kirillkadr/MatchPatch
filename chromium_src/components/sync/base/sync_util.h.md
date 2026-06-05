### match
```cpp
...
#define COMPONENTS_SYNC_BASE_SYNC_UTIL_H_

 #include <string>
 
 >>> 
#include "components/version_info/channel.h"

 ... 
```
### patch
```cpp
#include "brave/components/brave_sync/buildflags.h"

```

### match
```cpp
...
 namespace 
 internal 
 { 
 >>> 
// Default sync server URL. Visible for testing.
 ... } ...  
```
### patch
```cpp
inline constexpr char kSyncServerUrl[] = BUILDFLAG(BRAVE_SYNC_ENDPOINT);
inline constexpr char kSyncDevServerUrl[] = BUILDFLAG(BRAVE_SYNC_ENDPOINT);

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 namespace internal { ... 
>>> 
 inline 
 constexpr 
 char 
 kSyncServerUrl[] 
 = 
<<< 
"https://clients4.google.com/chrome-sync"
 ... } ...  } ...  
```
### patch
```cpp
inline constexpr char kSyncServerUrl_ChromiumImpl[] =

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 namespace internal { ... 
>>> 
 inline 
 constexpr 
 char 
 kSyncDevServerUrl[] 
 = 
<<< 
"https://clients4.google.com/chrome-sync/dev"
 ... } ...  } ...  
```
### patch
```cpp
inline constexpr char kSyncDevServerUrl_ChromiumImpl[] =

```

