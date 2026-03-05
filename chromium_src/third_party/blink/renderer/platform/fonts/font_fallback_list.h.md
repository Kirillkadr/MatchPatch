### match
```
...
 # ifndef ... 
 #define THIRD_PARTY_BLINK_RENDERER_PLATFORM_FONTS_FONT_FALLBACK_LIST_H_
 
 >>> 
#include "third_party/blink/renderer/platform/fonts/font_cache.h"

 ... 
```
### patch
```
#include "base/functional/callback.h"
#include "third_party/blink/renderer/platform/platform_export.h"
#include "third_party/blink/renderer/platform/wtf/text/atomic_string.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class PLATFORM_EXPORT FontFallbackList
    : public GarbageCollected<FontFallbackList> { ... 
AtomicString emphasis_mark_text_;
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```
class ExecutionContext;
}
namespace brave {

typedef base::RepeatingCallback<bool(blink::ExecutionContext*,
                                     const blink::AtomicString&)>
    AllowFontFamilyCallback;

PLATFORM_EXPORT void RegisterAllowFontFamilyCallback(
    AllowFontFamilyCallback callback);

}  // namespace brave

```

