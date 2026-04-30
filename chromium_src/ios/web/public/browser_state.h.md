### match
```cpp
...
 
 # ifndef ... 
#include "services/network/public/mojom/proxy_resolving_socket.mojom.h"

 #include "services/network/public/mojom/url_loader_factory.mojom.h"
 
 >>> 
namespace base {
class FilePath;
}
 ... 
```
### patch
```cpp
class PrefService;
// This override is tied to the replaced implementation of `//ios/web_view`'s
// CWVWebViewConfiguration (see cwv_web_view_configuration_internal.h override)
//
// Since this replaced implementation replaces WebViewBrowserState with
// web::BrowserState, there are a few places that use the GetPrefs method
// exposed on WebViewBrowserState.
//
// This adds a `GetPrefs` method to the public web::BrowserState definition
// to avoid build failures, even though the code that is calling it will never
// be used by us.

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace web { ... 
// Returns a URLLoaderFactory that is backed by GetRequestContext.
 network::mojom::URLLoaderFactory* GetURLLoaderFactory(); 
 >>> 
// Returns a CookieManager that is backed by GetRequestContext.
 ... } ...  
```
### patch
```cpp
  PrefService* GetPrefs() {
    NOTREACHED();
    return nullptr;
  }
  void Unused();

```

