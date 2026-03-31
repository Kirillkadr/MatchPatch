### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include "base/functional/callback_forward.h"
 
 >>> 
class GURL
 ... 
```
### patch
```cpp
#include "chrome/browser/notifications/notification_handler_impl.h"

```

### match
```cpp
...
 
 # ifndef ...   >>> 
 class 
 NotificationHandler 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
class NotificationHandler_ChromiumImpl {

```

### match
```cpp
...
 
 # ifndef ... 
 
 class NotificationHandler_ChromiumImpl { ... 
enum class Type {
    WEB_PERSISTENT = 0,
    WEB_NON_PERSISTENT = 1,
    EXTENSION = 2,
    // SEND_TAB_TO_SELF = 3,  // Deprecated.
    TRANSIENT = 4,  // A generic type for any notification that does not outlive
                    // the browser instance and is controlled by a
                    // NotificationDelegate.
    // Deprecated
    // PERMISSION_REQUEST = 5,  // A permission request that is presented to the
    //                          // user via a notification.
    SHARING = 6,
    ANNOUNCEMENT = 7,
    NEARBY_SHARE = 8,
    NOTIFICATIONS_MUTED = 9,
    TAILORED_SECURITY = 10,
    DEFAULT_BROWSER_CHANGED = 11,
    MAX = DEFAULT_BROWSER_CHANGED,
  };  >>> 
 virtual ~NotificationHandler();  <<< 
// Called after a notification has been displayed.
 ... } ...  
```
### patch
```cpp
  virtual ~NotificationHandler_ChromiumImpl();

```

