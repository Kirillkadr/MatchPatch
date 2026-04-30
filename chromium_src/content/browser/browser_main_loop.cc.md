### match
```cpp
...
#include "sql/sql_memory_dump_provider.h"

 #include "ui/base/clipboard/clipboard.h"
 
 >>> 
#include "ui/display/display_features.h"

 ...
```
### patch
```cpp
#if BUILDFLAG(IS_ANDROID)
#include "brave/content/browser/screen_orientation/brave_screen_orientation_delegate_android.h"
#endif

```

### match
```cpp
...
 
 namespace content { ... 
 
 void BrowserMainLoop::PostCreateMainMessageLoop() { ... 
 
 if (!parsed_command_line_->HasSwitch(
          switches::kDisableScreenOrientationLock)) { ...   >>> 
 std::make_unique<ScreenOrientationDelegateAndroid>() 
 ;  <<<  ...} ...  } ...  } ...
```
### patch
```cpp
        std::make_unique<BraveScreenOrientationDelegateAndroid>();

```

### match
```cpp
...
 ui::Clipboard::OnPreShutdownForCurrentThread(); 
 >>> 
 ...
```
### patch
```cpp
  if (parts_) {
    parts_->PreShutdown();
  }();

```

