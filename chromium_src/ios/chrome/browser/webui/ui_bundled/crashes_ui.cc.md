### match
```cpp
...
#include <memory>

 #include <vector>
 
 >>> 
#include "base/functional/bind.h"

 ... 
```
### patch
```cpp
#include "brave/components/version_info/version_info.h"
#include "components/version_info/version_info.h"

```

### match
```cpp
...
 
 void CrashesDOMHandler::UpdateUI() { ... 
result.Set("crashes", std::move(crash_list));  >>> 
 result.Set("version", version_info::GetVersionNumber());  <<< 
result.Set("os", base::SysInfo::OperatingSystemName() + " " +
                       base::SysInfo::OperatingSystemVersion());
 ... } ...  
```
### patch
```cpp
  result.Set("version", version_info::GetBraveVersionNumberForDisplay());

```

