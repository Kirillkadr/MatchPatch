### match
```cpp
...
 
 # ifndef ... 
#import "ios/web_view/internal/web_view_browser_state.h"

 #import "url/gurl.h"
 
 >>> 
namespace autofill {
class LogRouter;
}
 ... 
```
### patch
```cpp
class BraveWebViewPasswordManagerClient;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace ios_web_view { ... 
const password_manager::SyncCredentialsFilter credentials_filter_;
 password_manager::PasswordRequirementsService* requirements_service_; 
 >>> 
// The preference associated with
 ... } ...  
```
### patch
```cpp
  friend class ::BraveWebViewPasswordManagerClient;

```

