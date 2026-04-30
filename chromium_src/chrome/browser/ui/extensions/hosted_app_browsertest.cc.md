### match
```cpp
...
#include "base/test/scoped_feature_list.h"

 #include "base/values.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/brave_content_browser_client.h"

```

### match
```cpp
...
>>>
 class 
 JitChromeContentBrowserClient 
 : public ChromeContentBrowserClient 
 {  <<< 
public
 ... } ...  
```
### patch
```cpp
    class JitChromeContentBrowserClient : public BraveContentBrowserClient {

```

