### match
```cpp
...
 
 # ifndef ... 
#include <utility>

 #include "base/callback_list.h"
 
 >>> 
#include "base/memory/raw_ptr.h"

 ... 
```
### patch
```cpp
#include "base/debug/stack_trace.h"

```

### match
```cpp
...
 
 # ifndef ... 
#include "printing/buildflags/buildflags.h"

 #include "services/network/public/cpp/network_quality_tracker.h"
 
 >>> 
#include "ui/base/unowned_user_data/unowned_user_data_host.h"

 ... 
```
### patch
```cpp
#include "services/network/public/mojom/network_service.mojom-forward.h"

```

### match
```cpp
...
 
 # ifndef ... 
#include "services/network/public/mojom/network_service.mojom-forward.h"

 #include "ui/base/unowned_user_data/unowned_user_data_host.h"
 
 >>> 
#if !BUILDFLAG(IS_ANDROID)
#include "chrome/browser/upgrade_detector/build_state.h"
#endif
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)
#define StartTearDown virtual StartTearDown
#define PostDestroyThreads virtual PostDestroyThreads
#endif  // !BUILDFLAG(IS_ANDROID)


```

### match
```cpp
...
 
 # ifndef ... 
// Called to complete initialization.  >>> 
 void Init();  <<< 
#if !BUILDFLAG(IS_ANDROID)
  // Sets a closure to be run to break out of a run loop on browser shutdown
  // (when the KeepAlive count reaches zero).
  // TODO(crbug.com/41390731): This is also used on macOS for the Cocoa
  // first run dialog so that shutdown can be initiated via a signal while the
  // first run dialog is showing.
  void SetQuitClosure(base::OnceClosure quit_closure);
#endif
 ... 
```
### patch
```cpp
  void virtual Init();

```

### match
```cpp
...
 
 # ifndef ... 
// requires all threads running.  >>> 
 void PreMainMessageLoopRun();  <<< 
// Most cleanup is done by these functions, driven from
 ... 
```
### patch
```cpp
  void virtual PreMainMessageLoopRun();

```

### match
```cpp
...
 #endif 
 // CHROME_BROWSER_BROWSER_PROCESS_IMPL_H_ 
 >>> 
 ... 
```
### patch
```cpp

#undef PostDestroyThreads
#undef StartTearDown
```

