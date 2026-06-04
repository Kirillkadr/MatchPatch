### match
```cpp
...
// found in the LICENSE file.
 #include "components/omnibox/browser/verbatim_match.h"
 
 >>> 
#include "base/containers/fixed_flat_set.h"

 ... 
```
### patch
```cpp
#include "content/public/common/url_constants.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 #if BUILDFLAG(IS_ANDROID ) ... 
 
 base::MakeFixedFlatSet<std::string_view> ( ...   >>> 
 content::kChromeUIScheme 
 ,  <<< 
#if
 ... ) ...  } ...  
```
### patch
```cpp
        content::kChromeUIScheme, content::kBraveUIScheme,

```

