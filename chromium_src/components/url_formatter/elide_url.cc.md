### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ...
```
### patch
```cpp
#include "components/url_formatter/elide_url.h"

```

### match
```cpp
...
>>>
 std::u16string 
 FormatOriginForSecurityDisplay 
 ( 
<<< 
...) ...
```
### patch
```cpp
std::u16string FormatOriginForSecurityDisplay_ChromiumImpl(

```

### match
```cpp
...

  if (url_subdomain) {
    const size_t domain_start_index = url_host->find(*url_domain);
    constexpr std::u16string_view kWwwPrefix = u"www.";
    if (domain_start_index != std::u16string::npos) {
      *url_subdomain = url_host->substr(0, domain_start_index);
    }
    if ((*url_subdomain == kWwwPrefix || url_subdomain->empty() ||
         url.SchemeIsFile())) {
      url_subdomain->clear();
    }
  }

 } 
 >>> 
 ...
```
### patch
```cpp
std::u16string FormatOriginForSecurityDisplay(
    const url::Origin& origin,
    const SchemeDisplay scheme_display) {
  const url::Origin updated_origin = url::Origin::CreateFromNormalizedTuple(
      origin.scheme() == "chrome" ? "brave" : origin.scheme(), origin.host(),
      origin.port());
  return FormatOriginForSecurityDisplay_ChromiumImpl(updated_origin,
                                                     scheme_display);
}

```

