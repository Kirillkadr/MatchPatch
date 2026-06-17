### match
```cpp
...
// found in the LICENSE file.
 #include "components/test/components_test_suite.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "ui/base/resource/resource_bundle.h"

```

### match
```cpp
...

>>> 
 pak_path.AppendASCII("components_tests_resources.pak") 
 , 
<<< 
... ...
```
### patch
```cpp
pak_path.AppendASCII("brave_components_tests_resources.pak"),
      ui::kScaleFactorNone);
  ui::ResourceBundle::GetSharedInstance().AddDataPackFromPath(pak_path.AppendASCII("components_tests_resources.pak"),

```

