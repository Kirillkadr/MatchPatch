### match
```
...
// found in the LICENSE file.
 #include "chrome/browser/history_embeddings/history_embeddings_utils.h"
 
 >>> 
#include "chrome/browser/browser_process.h"

 ...
```
### patch
```
#include "base/feature_override.h"

```

### match
```
...
 
 namespace history_embeddings { ... 
 
 >>> 
 } ...
```
### patch
```
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kLaunchedHistoryEmbeddings, base::FEATURE_DISABLED_BY_DEFAULT},
}});


```

