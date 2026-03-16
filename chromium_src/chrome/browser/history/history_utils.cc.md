### match
```
...
// found in the LICENSE file.
 #include "chrome/browser/history/history_utils.h"
 
 >>> 
#include "chrome/common/url_constants.h"

 ...
```
### patch
```
#include "brave/components/constants/url_constants.h"

```

### match
```
...
#include "chrome/common/url_constants.h"

 #include "components/dom_distiller/core/url_constants.h"
 
 >>> 
#include "url/gurl.h"

 ...
```
### patch
```
#include "extensions/buildflags/buildflags.h"

```

### match
```
...
>>>
 bool 
 CanAddURLToHistory(const GURL& url) 
 {  <<< 
if (!url.is_valid())
    return false;
 ... } ...
```
### patch
```
bool CanAddURLToHistory_ChromiumImpl(const GURL& url) {

```

### match
```
...
 
 bool CanAddURLToHistory_ChromiumImpl(const GURL& url) {
  if (!url.is_valid())
    return false;
 >>>
```
### patch
```
bool CanAddURLToHistory(const GURL& url) {
  if (!CanAddURLToHistory_ChromiumImpl(url))
    return false;
  bool is_brave_scheme = url.SchemeIs(content::kBraveUIScheme);
  return !is_brave_scheme;
}

```

