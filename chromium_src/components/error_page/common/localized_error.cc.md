### match
```cpp
...
// found in the LICENSE file.
 #include "components/error_page/common/localized_error.h"
 
 >>> 
#include <stddef.h>

 ...
```
### patch
```cpp
#include "components/grit/brave_components_strings.h"
#include "components/url_formatter/url_formatter.h"
#include "url/gurl.h"

```

### match
```cpp
...
 namespace 
 error_page 
 { 
 >>> 
namespace {

 ... } ...
```
### patch
```cpp
std::u16string GetFailedUrlString(GURL failed_url);

```

### match
```cpp
...
 >>>
std::u16string GetStringWithPlaceholder(int resource_id,
                                        std::u16string host_name,
                                        std::u16string failed_url_string) 
 ...
```
### patch
```cpp
#define failed_url_string(FORMATTED_URL) \
  failed_url_string = error_page::GetFailedUrlString(failed_url);

```

### match
```cpp
...
 
 namespace error_page { ... 
 
 LocalizedError::PageState LocalizedError::GetPageStateForOverriddenErrorPage(
    base::DictValue string_dict,
    int error_code,
    const std::string& error_domain,
    const GURL& failed_url,
    const std::string& locale) { ... 
return result;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
#undef failed_url_string

```

### match
```cpp
...
 
 namespace error_page { ... 
 
 bool LocalizedError::IsBlockedByAdministratorError(int error_code) { ... 
return error_code == net::ERR_BLOCKED_BY_ADMINISTRATOR ||
         error_code == net::ERR_BLOCKED_IN_INCOGNITO_BY_ADMINISTRATOR;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
constexpr char kBraveUIScheme[] = "brave";
}
std::u16string GetFailedUrlString(GURL failed_url) {
  if (failed_url.scheme() == kChromeUIScheme) {
    GURL::Replacements replacements;
    replacements.SetSchemeStr(kBraveUIScheme);

    failed_url = failed_url.ReplaceComponents(replacements);
  }

  return url_formatter::FormatUrl(
      failed_url, url_formatter::kFormatUrlOmitNothing,
      base::UnescapeRule::NORMAL, nullptr, nullptr, nullptr);
}

```

