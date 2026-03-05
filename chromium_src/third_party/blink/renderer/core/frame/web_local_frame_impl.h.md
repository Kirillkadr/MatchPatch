### match
```
...
 # ifndef ... 
#include <utility>

 #include <vector>
 
 >>> 
#include "base/dcheck_is_on.h"

 ... 
```
### patch
```
#include "third_party/blink/public/web/web_local_frame.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 bool did_navigate 
 ) 
 override 
 ; 
 >>> 
 ... } ...  
```
### patch
```
  void SetOriginForClearWindowNameCheck(const url::Origin&)

```

