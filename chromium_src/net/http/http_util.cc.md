### match
```
...
// http://lxr.mozilla.org/mozilla/source/netwerk/base/src/nsURLHelper.cpp#834
 #include "net/http/http_util.h"
 
 >>> 
#include <algorithm>

 ...
```
### patch
```
#include "net/http/http_util.h"

#include "base/strings/string_util.h"

```

### match
```
...
 namespace net { ...   >>> 
 bool 
 HttpUtil::IsNonCoalescingHeader(std::string_view name) 
 {  <<< ... 
// NOTE: "set-cookie2" headers do not support expires attributes, so we don't
 ... } ...  } ...
```
### patch
```
bool HttpUtil::IsNonCoalescingHeader_ChromiumImpl(std::string_view name) {

```

### match
```
...
 >>>
```
### patch
```
// static
bool HttpUtil::IsNonCoalescingHeader(std::string_view name) {
  if (base::EqualsCaseInsensitiveASCII(name, "onion-location")) {
    return true;
  }
  return IsNonCoalescingHeader_ChromiumImpl(name);
}

```
