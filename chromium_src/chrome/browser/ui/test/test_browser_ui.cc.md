### match
```cpp
...
#include <optional>

 #include "base/command_line.h"
 
 >>> 
#include "base/test/gtest_util.h"

 ... 
```
### patch
```cpp
#include "base/logging.h"

```

### match
```cpp
...
#include "base/test/test_switches.h"

 #include "build/build_config.h"
 
 >>> 
#include "ui/base/ui_base_features.h"

 ... 
```
### patch
```cpp
#include "testing/gtest/include/gtest/gtest.h"

```

### match
```cpp
...
 
 void TestBrowserUi::ShowAndVerifyUi() { ... 
 
 if (!IsInteractiveUi() &&
      !base::CommandLine::ForCurrentProcess()->HasSwitch(
          switches::kForceDarkMode) &&
      ui::NativeTheme::GetInstanceForNativeUi()->preferred_color_scheme() ==
          ui::NativeTheme::PreferredColorScheme::kDark) { ...   >>> 
 GTEST_SKIP() << "Host is in dark mode; skipping test";  <<<  ...} ...  } ...  
```
### patch
```cpp
    LOG(WARNING) << "Brave: forcing test to run. Original Chromium behavior: "() << "Host is in dark mode; skipping test";

```

