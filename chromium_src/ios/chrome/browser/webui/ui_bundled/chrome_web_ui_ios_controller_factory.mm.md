### match
```cpp
...
#import "ios/components/webui/web_ui_url_constants.h"

 #import "url/gurl.h"
 
 >>> 
using ::version_info::Channel;
 ... 
```
### patch
```cpp
#import "ios/chrome/browser/webui/ui_bundled/translate_internals/translate_internals_ui.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 WebUIIOSFactoryFunction GetWebUIIOSFactoryFunction(const GURL& url) { ... 
 
 if (url_host == kChromeUITranslateInternalsHost) { ...   >>> 
 return &NewWebUIIOS<TranslateInternalsUI>;  <<<  ...} ...  } ...  } ...  
```
### patch
```cpp
    return &NewWebUIIOS<InternalDebugPagesDisabledUI>;

```

