### match
```cpp
...
#include "base/logging.h"

 #include "base/strings/string_util.h"
 
 >>> 
#include "build/build_config.h"

 ...
```
### patch
```cpp
#include "brave/components/constants/url_constants.h"

```

### match
```cpp
...
>>>
 bool 
 ProfileIOData::IsHandledProtocol(std::string_view scheme) 
 {  <<< 
DCHECK_EQ(scheme, base::ToLowerASCII(scheme));
 ... } ...
```
### patch
```cpp
bool ProfileIOData::IsHandledProtocol_ChromiumImpl(std::string_view scheme) {

```

### match
```cpp
...
 
// static  >>> 
 bool ProfileIOData::IsHandledURL(const GURL& url 
 ) 
  
 {  <<< 
 ...
```
### patch
```cpp
bool ProfileIOData::IsHandledURL_ChromiumImpl(const GURL& url) {

```

### match
```cpp
...
  >>> 
 return IsHandledProtocol(url.GetScheme());  <<<  ...
```
### patch
```cpp
return IsHandledProtocol_ChromiumImpl(url.GetScheme());
}

bool ProfileIOData::IsHandledProtocol(std::string_view scheme) {
  if (scheme == kBraveUIScheme)
    return true;
  return IsHandledProtocol_ChromiumImpl(scheme);
}

// We need to provide our own version of IsHandledURL() as well to make sure
// that we get our own version of IsHandledProtocol() called when invoked via
// IsHandledURL(). Otherwise the old version will still be called since the
// renaming of IsHandledProtocol above does also modify the call point.
bool ProfileIOData::IsHandledURL(const GURL& url) {
  if (!url.is_valid()) {
    // We handle error cases.
    return true;
  }
  return IsHandledProtocol(url.scheme());

```

