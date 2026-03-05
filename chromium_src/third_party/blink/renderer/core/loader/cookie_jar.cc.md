### match
```
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "third_party/blink/renderer/core/loader/cookie_jar.h"

 ...
```
### patch
```
#include "third_party/blink/renderer/core/loader/cookie_jar.h"

```

### match
```
...
#include "third_party/blink/renderer/core/loader/cookie_jar.h"

 #include "third_party/blink/renderer/core/loader/cookie_jar.h"
 
 >>> 
#include <cstdint>

 ...
```
### patch
```
#include "mojo/public/cpp/base/shared_memory_version.h"

```

### match
```
...
 if (shared_memory_version_client_->SharedVersionIsGreaterThan(   >>> 
 last_version_ 
 ) 
 ) 
 {  <<< ... 
return true;
 ... } ...
```
### patch
```
          mojo::shared_memory_version::kInvalidVersion)) {

```

