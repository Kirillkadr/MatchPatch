### match
```
...
#include "third_party/blink/renderer/platform/heap/garbage_collected.h"

 #include "third_party/blink/renderer/platform/wtf/text/wtf_string.h"
 
 >>> 
// Populates all parameters for texImage2D, including width, height, depth (set
 ... ) ...  
```
### patch
```
#include <algorithm>
#include "base/notreached.h"
#include "brave/third_party/blink/renderer/core/farbling/brave_session_cache.h"
#include "third_party/blink/renderer/bindings/modules/v8/webgl_any.h"

using blink::ExecutionContext;
using blink::ScriptState;
using blink::ScriptValue;
using blink::WebGL2RenderingContextBase;
using blink::WebGLAny;

namespace {

ScriptValue FarbleGLIntParameter(WebGL2RenderingContextBase* owner,
                                 ScriptState* script_state,
                                 GLenum pname,
                                 int discard) {
  GLint value = 0;
  if (!owner->isContextLost())
    owner->ContextGL()->GetIntegerv(pname, &value);
  if (value > 0) {
    brave::FarblingPRNG prng =
        brave::BraveSessionCache::From(*ExecutionContext::From(script_state))
            .MakePseudoRandomGenerator();
    prng.discard(discard);
    if (prng() % 2 != 0) {
      value = value - 1;
    }
  }
  return WebGLAny(script_state, value);
}

ScriptValue FarbleGLInt64Parameter(WebGL2RenderingContextBase* owner,
                                   ScriptState* script_state,
                                   GLenum pname,
                                   int discard) {
  GLint64 value = 0;
  if (!owner->isContextLost())
    owner->ContextGL()->GetInteger64v(pname, &value);
  if (value > 0) {
    brave::FarblingPRNG prng =
        brave::BraveSessionCache::From(*ExecutionContext::From(script_state))
            .MakePseudoRandomGenerator();
    prng.discard(discard);
    if (prng() % 2 != 0) {
      value = value - 1;
    }
  }
  return WebGLAny(script_state, value);
}

}  // namespace

```

