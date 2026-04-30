### match
```cpp
...
#include "components/permissions/bluetooth_scanning_prompt_controller.h"

 #include <algorithm>
 
 >>> 
#include "base/strings/utf_string_conversions.h"

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
 
 namespace permissions { ... 
std::pair<std::u16string, std::u16string>  >>> 
 BluetoothScanningPromptController::GetThrobberLabelAndTooltip() const 
 {  <<< 
return {
      l10n_util::GetStringUTF16(IDS_BLUETOOTH_DEVICE_CHOOSER_SCANNING_LABEL),
      l10n_util::GetStringUTF16(
          IDS_BLUETOOTH_DEVICE_CHOOSER_SCANNING_LABEL_TOOLTIP)};
 ... } ...  } ...  
```
### patch
```cpp
BluetoothScanningPromptController::GetThrobberLabelAndTooltip() const override; 
  std::optional<ChooserControllerType> GetType() const {

```

