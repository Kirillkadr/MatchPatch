### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/permissions/chooser_controller.h"

 ... 
```
### patch
```cpp
#include "components/permissions/chooser_controller.h"

```

### match
```cpp
...
#include "components/permissions/chooser_controller.h"

 #include "components/permissions/chooser_controller.h"
 
 >>> 
#include "base/notreached.h"

 ... 
```
### patch
```cpp
#include <optional>

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 int ChooserController::GetAuthorizeBluetoothLinkTextMessageId() const { ... 
NOTREACHED();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
std::optional<ChooserControllerType> ChooserController::GetType() const {
  return std::nullopt;
}

```

