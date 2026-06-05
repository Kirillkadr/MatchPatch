### match
```cpp
...
// found in the LICENSE file.
 #include "components/sync/engine/net/sync_server_connection_manager.h"
 
 >>> 
#include <stdint.h>

 ... 
```
### patch
```cpp
#include "net/http/http_request_headers.h"

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 namespace { ... 
 
 HttpResponse Connection::PostRequestAndDownloadResponse(
    const GURL& sync_request_url,
    const std::string& access_token,
    const std::string& payload,
    std::string* buffer_out) { ... 
 
 if (!access_token.empty()) { ... 
net::HttpRequestHeaders headers;
>>> 
 headers.SetHeader("Authorization", "Bearer " + access_token); 
<<< 
post_provider_->SetExtraRequestHeaders(headers);
 ... } ...  } ...  } ...  } ...  
```
### patch
```cpp
    headers.AddHeadersFromString(std::string("Authorization") + std::string(": ") +
                       std::string("Bearer " + access_token));

```

