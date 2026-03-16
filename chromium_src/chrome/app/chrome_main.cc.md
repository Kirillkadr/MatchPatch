### match
```
...
#include "content/public/common/content_switches.h"

 #include "partition_alloc/buildflags.h"
 
 >>> 
#if BUILDFLAG(IS_MAC)
#include "chrome/app/chrome_main_mac.h"
#endif
 ...
```
### patch
```
#include "brave/app/brave_main_delegate.h"

```

### match
```
...
 int ChromeMain(int argc, const char** argv) { ... 
 #if BUILDFLAG(IS_WIN ) ... 
StartupTimestamps timestamps{
      base::TimeTicks::FromInternalValue(exe_entry_point_ticks),
      base::TimeTicks::FromInternalValue(preread_begin_ticks),
      base::TimeTicks::FromInternalValue(preread_end_ticks)};  >>> 
 ChromeMainDelegate chrome_main_delegate(timestamps);  <<< ... 
#else  // BUILDFLAG(IS_WIN)
  ChromeMainDelegate chrome_main_delegate(
      {.exe_entry_point_ticks = base::TimeTicks::Now()});
 ... } ...
```
### patch
```
  BraveMainDelegate chrome_main_delegate(timestamps);

```

### match
```
...
 #else  // BUILDFLAG(IS_WIN)  >>> 
 ChromeMainDelegate 
 chrome_main_delegate 
 (  <<< ... 
{.exe_entry_point_ticks = base::TimeTicks::Now()}
 ... ) ...
```
### patch
```
  BraveMainDelegate chrome_main_delegate(

```

