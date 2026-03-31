### match
```cpp
...
// found in the LICENSE file.
 #include "content/shell/browser/shell_permission_manager.h"
 
 >>> 
#include "base/command_line.h"

 ... 
```
### patch
```cpp
#include "components/permissions/permission_util.h"
#include "third_party/blink/public/common/permissions/permission_utils.h"

```

### match
```cpp
...
 
 namespace content { ... 
 
 namespace { ... 
 
 bool IsAllowlistedPermissionType(PermissionType permission) { ... 
case PermissionType::CLIPBOARD_READ_WRITE:
 case PermissionType::CLIPBOARD_SANITIZED_WRITE: 
 >>> 
case PermissionType::NUM:
 ... } ...  } ...  } ...  
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
  case PermissionType::BRAVE_CARDANO:
  case PermissionType::BRAVE_GOOGLE_SIGN_IN:
  case PermissionType::BRAVE_OPEN_AI_CHAT:

```

