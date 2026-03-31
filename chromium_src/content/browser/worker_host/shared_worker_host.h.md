### match
```cpp
...
 
 # ifndef ... 
 #define CONTENT_BROWSER_WORKER_HOST_SHARED_WORKER_HOST_H_
 
 >>> 
#include <list>

 ... 
```
### patch
```cpp
#include "brave/components/brave_shields/core/common/shields_settings.mojom.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
void CreateCodeCacheHost(
      mojo::PendingReceiver<blink::mojom::CodeCacheHost> receiver);
 // Creates a network factory params for subresource requests from this worker. 
 >>> 
network::mojom::URLLoaderFactoryParamsPtr
  CreateNetworkFactoryParamsForSubresources();
 ... } ...  
```
### patch
```cpp
  network::mojom::URLLoaderFactoryParamsPtr
  UnusedFunction();                                                      
  void GetBraveShieldsSettings(
      const GURL& url,
      base::OnceCallback<void(brave_shields::mojom::ShieldsSettingsPtr)>
          callback);

```

