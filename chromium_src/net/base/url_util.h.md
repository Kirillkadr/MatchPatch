### match
```
...
 # ifndef ... 
#include <string>

 #include <string_view>
 
 >>> 
#include "base/memory/raw_ref.h"

 ... 
```
### patch
```
#include "net/base/net_export.h"
#include "url/origin.h"

```

### match
```
...
 # ifndef ... 
 namespace net { ... 
 std::string_view input 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```
// Convert this URL into an encoded storage domain string, which is used
// to identify a particular storage domain uniquely in a BrowserContext.
NET_EXPORT std::string URLToEphemeralStorageDomain(const GURL& url);

NET_EXPORT bool IsOnion(const GURL& url);

NET_EXPORT bool IsOnion(const url::Origin& origin);

NET_EXPORT bool IsLocalhostOrOnion(const GURL& url);

```

