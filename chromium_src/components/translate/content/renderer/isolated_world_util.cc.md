### match
```cpp
...
// found in the LICENSE file.
 #include "components/translate/content/renderer/isolated_world_util.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/components/translate/core/common/brave_translate_features.h"
#include "third_party/blink/public/platform/web_isolated_world_info.h"

```

### match
```cpp
...
 
 namespace translate { ... 
 
 void EnsureIsolatedWorldInitialized(int world_id) { ... 
>>> 
 blink::SetIsolatedWorldInfo(world_id, info); 
<<< 
...} ...  } ...  
```
### patch
```cpp
  blink::AdjustedSetIsolatedWorldInfo(world_id, info);

```

### match
```cpp
...
 
 namespace translate { ... 
 } 
 // namespace translate 
 >>> 
 ... 
```
### patch
```cpp
namespace blink {
namespace {

void AdjustedSetIsolatedWorldInfo(int32_t world_id,
                                  const blink::WebIsolatedWorldInfo& info) {
  blink::WebIsolatedWorldInfo new_info(info);
  // Limit all network requests to the security origin.
  if (!translate::UseGoogleTranslateEndpoint()) {
    new_info.content_security_policy =
        "default-src 'none'; frame-ancestors 'none'; base-uri 'none';"
        "style-src 'self' 'unsafe-inline';"
        "connect-src 'self';"
        "script-src 'self' 'unsafe-eval' 'unsafe-inline';"
        "img-src 'self' data:";
  }
  blink::AdjustedSetIsolatedWorldInfo(world_id, new_info);
}

}  // namespace
}  // namespace blink
```

