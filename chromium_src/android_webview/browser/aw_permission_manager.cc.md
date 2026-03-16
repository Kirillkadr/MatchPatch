### match
```
...
#include "components/permissions/permission_manager.h"

 #include "components/permissions/permission_util.h"
 
 >>> 
#include "content/public/browser/child_process_security_policy.h"

 ...
```
### patch
```
#include "brave/components/brave_wallet/common/buildflags/buildflags.h"
#include "components/permissions/permission_util.h"

```

### match
```
...
#include "third_party/blink/public/common/features.h"

 #include "third_party/blink/public/common/permissions/permission_utils.h"
 
 >>> 
using blink::PermissionType;
 ...
```
### patch
```
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
#define BRAVE_WALLET_PERMISSION_TYPES  \
  case PermissionType::BRAVE_ETHEREUM: \
  case PermissionType::BRAVE_SOLANA:   \
  case PermissionType::BRAVE_CARDANO:
#else
#define BRAVE_WALLET_PERMISSION_TYPES
#endif


```

### match
```
...
 namespace android_webview { ... 
 void AwPermissionManager::RequestPermissions(
    content::RenderFrameHost* render_frame_host,
    const content::PermissionRequestDescription& request_description,
    base::OnceCallback<void(const std::vector<content::PermissionResult>&)>
        callback) { ... 
 case PermissionType : ... 
pending_request_raw->SetPermissionResult(
            permissions[i],
            content::PermissionResult(PermissionStatus::GRANTED));
 break; 
 >>> 
 case PermissionType::NUM:

 ... } ...  } ...
```
### patch
```
      case PermissionType::BRAVE_ADS:
      case PermissionType::BRAVE_TRACKERS:
      case PermissionType::BRAVE_HTTP_UPGRADABLE_RESOURCES:
      case PermissionType::BRAVE_FINGERPRINTING_V2:
      case PermissionType::BRAVE_SHIELDS:
      case PermissionType::BRAVE_REFERRERS:
      case PermissionType::BRAVE_COOKIES:
      case PermissionType::BRAVE_SPEEDREADER:
      BRAVE_WALLET_PERMISSION_TYPES
      case PermissionType::BRAVE_GOOGLE_SIGN_IN:
      case PermissionType::BRAVE_OPEN_AI_CHAT:

```

### match
```
...
 namespace android_webview { ... 
 PermissionStatus AwPermissionManager::GetPermissionStatusInternal(
    const blink::mojom::PermissionDescriptorPtr& permission_descriptor,
    const GURL& requesting_origin,
    const GURL& embedding_origin,
    content::WebContents* web_contents) { ... 
case blink::PermissionType::NOTIFICATIONS:  >>> 
 case blink::PermissionType::NUM:  <<< ... 
case blink::PermissionType::PAYMENT_HANDLER:
 ... } ...  } ...  
```
### patch
```
    case blink::PermissionType::BRAVE_ADS:
    case PermissionType::BRAVE_TRACKERS:
    case PermissionType::BRAVE_HTTP_UPGRADABLE_RESOURCES:
    case PermissionType::BRAVE_FINGERPRINTING_V2:
    case PermissionType::BRAVE_SHIELDS:
    case PermissionType::BRAVE_REFERRERS:
    case PermissionType::BRAVE_COOKIES:
    case PermissionType::BRAVE_SPEEDREADER:
    BRAVE_WALLET_PERMISSION_TYPES
    case PermissionType::BRAVE_GOOGLE_SIGN_IN:
    case PermissionType::BRAVE_OPEN_AI_CHAT:
    case PermissionType::NUM:

```

### match
```
...
 namespace android_webview { ... 
 void AwPermissionManager::CancelPermissionRequest(int request_id) { ... 
 case PermissionType : ... 
// There is nothing to cancel so this is simply ignored.
 break; 
 >>> 
 ... } ...  } ...  
```
### patch
```
      case PermissionType::BRAVE_ADS:
      case PermissionType::BRAVE_TRACKERS:
      case PermissionType::BRAVE_HTTP_UPGRADABLE_RESOURCES:
      case PermissionType::BRAVE_FINGERPRINTING_V2:
      case PermissionType::BRAVE_SHIELDS:
      case PermissionType::BRAVE_REFERRERS:
      case PermissionType::BRAVE_COOKIES:
      case PermissionType::BRAVE_SPEEDREADER:
      BRAVE_WALLET_PERMISSION_TYPES
      case PermissionType::BRAVE_GOOGLE_SIGN_IN:
      case PermissionType::BRAVE_OPEN_AI_CHAT:

```