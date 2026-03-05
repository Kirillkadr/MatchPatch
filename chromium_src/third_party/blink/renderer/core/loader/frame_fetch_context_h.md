### match
```
...
 # ifndef ... 
#define THIRD_PARTY_BLINK_RENDERER_CORE_LOADER_FRAME_FETCH_CONTEXT_H_

 #include <optional>
 
 >>> 
#include "base/task/single_thread_task_runner.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/loader/base_fetch_context.h"
#include "third_party/blink/renderer/platform/loader/fetch/fetch_context.h"

```

### match
```
...
 bool 
 IsPrerendering() 
 const 
 override 
 ; 
 >>> 
bool
 ... 
```
### patch
```
  bool NotUsedOverride() {                                            \
    return false;                                                \
  }                                                              \
  String GetCacheIdentifierIfCrossSiteSubframe() const override; \
                                                                 \
 private:                                                        \
  mutable scoped_refptr<const SecurityOrigin>                    \
      top_frame_origin_for_cache_identifier_;                    \
  mutable String cache_identifier_if_cross_site_subframe_;       \
                                                                 \
 public:                                                         \

```

### match
```
...
>>>
 bool 
 AllowScript() 
 const 
 override 
 ;  <<< ... 
bool
 ... 
```
### patch
```
  bool AllowScript(const KURL& url) const override;

```

