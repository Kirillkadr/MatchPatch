### match
```cpp
...
// found in the LICENSE file.
 #include "content/browser/permissions/permission_controller_impl.h"
 
 >>> 
#include <optional>

 ...
```
### patch
```cpp
#include "content/browser/permissions/permission_util.h"
#include "third_party/blink/public/common/permissions/permission_utils.h"

```

### match
```cpp
...
 >>> 
case PermissionType::NUM:
 ...
```
### patch
```cpp
    case PermissionType::BRAVE_ADS:
  case PermissionType::BRAVE_TRACKERS:
  case PermissionType::BRAVE_HTTP_UPGRADABLE_RESOURCES:
  case PermissionType::BRAVE_FINGERPRINTING_V2:
  case PermissionType::BRAVE_SHIELDS:                   
  case PermissionType::BRAVE_REFERRERS:
  case PermissionType::BRAVE_COOKIES:
  case PermissionType::BRAVE_SPEEDREADER:
  case PermissionType::BRAVE_ETHEREUM:
  case PermissionType::BRAVE_SOLANA:
  case PermissionType::BRAVE_GOOGLE_SIGN_IN:
  case PermissionType::BRAVE_OPEN_AI_CHAT:
  case PermissionType::BRAVE_CARDANO:

```

