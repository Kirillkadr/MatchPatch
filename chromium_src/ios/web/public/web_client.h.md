### match
```cpp
...
 
 # ifndef ... 
 #define IOS_WEB_PUBLIC_WEB_CLIENT_H_
 
 >>> 
#import <Foundation/Foundation.h>

 ... 
```
### patch
```cpp
#import <Foundation/Foundation.h>

```

### match
```cpp
...
 
 # ifndef ... 
#import <Foundation/Foundation.h>

 #import <Foundation/Foundation.h>
 
 >>> 
#include <map>

 ... 
```
### patch
```cpp
#include "ios/web/common/user_agent.h"

```

### match
```cpp
...
 
 # ifndef ... 
 namespace 
 web 
 { 
 >>> 
class BrowserState
 ... } ...  
```
### patch
```cpp
class WebState;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace web { ... 
 
 class WebClient { ... 
// Returns true if browser lockdown mode is enabled. Default return value is
 // false. 
 >>> 
virtual bool IsBrowserLockdownModeEnabled();
 ... } ...  } ...  
```
### patch
```cpp
  virtual bool ShouldBlockJavaScript(web::WebState* web_state, NSURLRequest* request);
  virtual NSString* GetUserAgentForRequest(web::WebState* web_state,
                                           web::UserAgentType user_agent_type,
                                           NSURLRequest* request);
  virtual bool ShouldBlockUniversalLinks(web::WebState* web_state,
                                         NSURLRequest* request);

```

