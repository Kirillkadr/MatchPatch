### match
```cpp
...
 
 # ifndef ... 
#include <utility>

 #include <vector>
 
 >>> 
#include "base/memory/weak_ptr.h"

 ... 
```
### patch
```cpp
#include <optional>
#include "components/permissions/chooser_controller.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 
 class BluetoothChooserController : public ChooserController { ...   >>> 
 std::pair<std::u16string, std::u16string> 
 GetThrobberLabelAndTooltip 
 ()  <<<  ...} ...  } ...  
```
### patch
```cpp
  std::pair<std::u16string, std::u16string> GetThrobberLabelAndTooltip() const override;
  std::optional<ChooserControllerType> GetType()

```

