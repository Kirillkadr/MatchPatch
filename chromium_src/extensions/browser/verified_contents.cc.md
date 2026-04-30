### match
```cpp
...
#include <algorithm>

 #include <string_view>
 
 >>> 
#include "base/base64url.h"

 ...
```
### patch
```cpp
#include "extensions/browser/verified_contents.h"
#include <memory>

#include "base/files/file_util.h"
#include "base/memory/ptr_util.h"
#include "extensions/common/extension.h"
```

### match
```cpp
...
   >>> 
 auto verified_contents = base::WrapUnique(new VerifiedContents(public_key));  <<< 
 ...
```
### patch
```cpp
  auto verified_contents = base::WrapUnique(Create_ChromiumImpl(new VerifiedContents(public_key), contents).release());
  if (verified_contents) {
    return verified_contents;
  }
  return Create_ChromiumImpl(
      new VerifiedContents(kBraveVerifiedContentsPublicKey), contents);
  }

  std::unique_ptr<VerifiedContents> VerifiedContents::Create_ChromiumImpl(
      VerifiedContents* vc, std::string_view contents) {                   
    std::unique_ptr<VerifiedContents> verified_contents(vc);
```