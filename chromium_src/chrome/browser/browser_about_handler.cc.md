### match
```cpp
...
#include "base/strings/string_util.h"

 #include "base/task/single_thread_task_runner.h"
 
 >>> 
#include "chrome/browser/lifetime/application_lifetime.h"

 ... 
```
### patch
```cpp
#include "brave/components/constants/url_constants.h"
#include "brave/components/constants/webui_url_constants.h"

```

### match
```cpp
...
>>>
 bool 
 HandleChromeAboutAndChromeSyncRewrite 
 (  <<< 
GURL* url
 ... ) ...  
```
### patch
```cpp
bool HandleChromeAboutAndChromeSyncRewrite_ChromiumImpl(

```

### match
```cpp
...
 
 bool HandleNonNavigationAboutURL(const GURL& url,
                                 content::BrowserContext* context) { ... 
NOTREACHED();
 } 
 >>> 
 ... 
```
### patch
```cpp
bool HandleChromeAboutAndChromeSyncRewrite(
    GURL* url,
    content::BrowserContext* browser_context) {
  if (url->SchemeIs(kBraveUIScheme)) {
    GURL::Replacements replacements;
    replacements.SetSchemeStr(content::kChromeUIScheme);
    *url = url->ReplaceComponents(replacements);
  }

  bool result =
      HandleChromeAboutAndChromeSyncRewrite_ChromiumImpl(url, browser_context);

  return result;
}

```

