### match
```cpp
...
#include "base/test/with_feature_override.h"

 #include "base/values.h"
 
 >>> 
#include "chrome/browser/chrome_content_browser_client.h"

 ... 
```
### patch
```cpp
#include "brave/browser/brave_content_browser_client.h"

```

### match
```cpp
...
 
 namespace { ...   >>> 
 class 
 MockChromeContentBrowserClient 
 : public ChromeContentBrowserClient 
 {  <<< 
public
 ... } ...  } ...  
```
### patch
```cpp
class MockChromeContentBrowserClient : public BraveContentBrowserClient {

```

### match
```cpp
...
 
 namespace { ... 
 
 class MockChromeContentBrowserClient : public BraveContentBrowserClient { ... 
 
 bool IsSharedStorageAllowed(
      content::BrowserContext* browser_context,
      content::RenderFrameHost* rfh,
      const url::Origin& top_frame_origin,
      const url::Origin& accessing_origin,
      std::string* out_debug_message,
      bool* out_block_is_site_setting_specific) override { ...   >>> 
 return 
 ChromeContentBrowserClient::IsSharedStorageAllowed 
 (  <<<  ...) ...  } ...  } ...  } ...  
```
### patch
```cpp
    return BraveContentBrowserClient::IsSharedStorageAllowed(

```

### match
```cpp
...
 
 namespace { ... 
 
 class MockChromeContentBrowserClient : public BraveContentBrowserClient { ... 
 
 bool IsSharedStorageSelectURLAllowed(
      content::BrowserContext* browser_context,
      const url::Origin& top_frame_origin,
      const url::Origin& accessing_origin,
      std::string* out_debug_message,
      bool* out_block_is_site_setting_specific) override { ...   >>> 
 return 
 ChromeContentBrowserClient::IsSharedStorageSelectURLAllowed 
 (  <<<  ...) ...  } ...  } ...  } ...  
```
### patch
```cpp
    return BraveContentBrowserClient::IsSharedStorageSelectURLAllowed(

```

