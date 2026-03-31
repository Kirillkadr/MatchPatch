### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "content/browser/renderer_host/mixed_content_checker.h"

 ... 
```
### patch
```cpp
#include "content/browser/renderer_host/mixed_content_checker.h"

```

### match
```cpp
...
 
 namespace content { ... 
 
 bool MixedContentChecker::IsMixedContentForTesting(const GURL& origin_url,
                                                   const GURL& url) { ... 
return IsMixedContent(origin, url);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// static
bool MixedContentChecker::DoesOriginSchemeRestrictMixedContent(
    const url::Origin& origin) {
  if (origin.host().ends_with(".onion") &&
      (origin.scheme() == url::kHttpsScheme ||
       origin.scheme() == url::kHttpScheme ||
       origin.scheme() == url::kWsScheme ||
       origin.scheme() == url::kWssScheme)) {
    return true;
  }
  return ::content::DoesOriginSchemeRestrictMixedContent(origin);
}

```

