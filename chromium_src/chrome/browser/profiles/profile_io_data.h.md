### match
```cpp
...
 
 # ifndef ... 
#define CHROME_BROWSER_PROFILES_PROFILE_IO_DATA_H_

 #include <string_view>
 
 >>> 
class GURL
 ... 
```
### patch
```cpp
#include "url/gurl.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ProfileIOData { ... 
// Returns true if |scheme| is handled in Chrome, or by default handlers in
 // net::URLRequest. 
 >>> 
static bool IsHandledProtocol(std::string_view scheme);
 ... } ...  
```
### patch
```cpp
  static bool  IsHandledProtocol_ChromiumImpl(std::string_view scheme); 

```


### match
```cpp
...
 
 # ifndef ... 
 
 class ProfileIOData { ... 
// Returns true if |url| is handled in Chrome, or by default handlers in
 // net::URLRequest. 
 >>> 
static bool IsHandledURL(const GURL& url);
 ... } ...  
```
### patch
```cpp
  static bool IsHandledURL_ChromiumImpl(const GURL& url);

```

