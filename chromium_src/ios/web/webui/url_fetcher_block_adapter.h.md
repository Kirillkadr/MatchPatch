### match
```cpp
...
 
 # ifndef ... 
#include <optional>

 #include <string>
 
 >>> 
#include "base/memory/scoped_refptr.h"

 ... 
```
### patch
```cpp
#include "base/memory/raw_ptr.h"
#include "services/network/public/mojom/url_response_head.mojom.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace web { ... 
// Callback for resource load.
 __strong web::URLFetcherBlockAdapterCompletion completion_handler_; 
 >>> 
// URLLoader for retrieving data from net stack.
 ... } ...  
```
### patch
```cpp

 public:
  const network::mojom::URLResponseHeadPtr getResponse() {
    return response_.Clone();
  }

 private:
  network::mojom::URLResponseHeadPtr response_;

```

