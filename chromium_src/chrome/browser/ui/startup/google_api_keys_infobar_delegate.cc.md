### match
```cpp
...
#include "google_apis/google_api_keys.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
// static
 ... 
```
### patch
```cpp
namespace google_apis {
constexpr char kBraveAPIKeysDevelopersHowToURL[] =
    "https://community.brave.app";
}  // namespace google_apis



```

### match
```cpp
...
 
 GURL GoogleApiKeysInfoBarDelegate::GetLinkURL() const { ...   >>> 
 return GURL(google_apis::kAPIKeysDevelopersHowToURL);  <<<  ...} ...  
```
### patch
```cpp
  return GURL(google_apis::kBraveAPIKeysDevelopersHowToURL);

```

