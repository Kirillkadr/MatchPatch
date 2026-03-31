### match
```cpp
...
#include "base/functional/callback.h"
  >>> 
 NotificationHandler::~NotificationHandler() = default;  <<< 
void NotificationHandler::OnShow(Profile* profile,
                                 const std::string& notification_id) {}
 ... 
```
### patch
```cpp
NotificationHandler_ChromiumImpl::~NotificationHandler_ChromiumImpl() = default;

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::OnShow 
 ( 
 Profile* profile 
 ,  <<< 
const std::string& notification_id
 ... ) ...  
```
### patch
```cpp

void NotificationHandler_ChromiumImpl::OnShow(Profile* profile,

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::OnClose 
 ( 
 Profile* profile 
 ,  <<< 
const GURL& origin
 ... ) ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::OnClose(Profile* profile,

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::OnClick 
 ( 
 Profile* profile 
 ,  <<< 
const GURL& origin
 ... ) ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::OnClick(Profile* profile,

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::DisableNotifications 
 (  <<< 
Profile* profile
 ... ) ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::DisableNotifications(

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::OpenSettings(Profile* profile, const GURL& origin) 
 {  <<< 
// Notification types that display a settings button must override this method
 ... } ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::OpenSettings(Profile* profile, const GURL& origin) {

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::ReportNotificationAsSafe 
 (  <<< 
const std::string& notification_id
 ... ) ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::ReportNotificationAsSafe(

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::ReportWarnedNotificationAsSpam 
 (  <<< 
const std::string& notification_id
 ... ) ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::ReportWarnedNotificationAsSpam(

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::ReportUnwarnedNotificationAsSpam 
 (  <<< 
const std::string& notification_id
 ... ) ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::ReportUnwarnedNotificationAsSpam(

```

### match
```cpp
...
>>>
 void 
 NotificationHandler::OnShowOriginalNotification 
 (  <<< 
const GURL& url
 ... ) ...  
```
### patch
```cpp
void NotificationHandler_ChromiumImpl::OnShowOriginalNotification(

```

