### match
```
...
#include <memory>

 #include <utility>
 
 >>> 
#include "base/bit_cast.h"

 ... 
```
### patch
```
#include <optional>

```

### match
```
...
#include "third_party/skia/include/core/SkImage.h"

 #include "ui/gfx/geometry/size.h"
 
 >>> 
// Populates parameters from texImage2D except for border, width, height, and
 ... 
```
### patch
```

#include "brave/third_party/blink/renderer/core/farbling/brave_session_cache.h"
#include "third_party/blink/renderer/core/dom/document.h"
#include "third_party/blink/renderer/core/frame/local_dom_window.h"
#include "third_party/blink/renderer/core/frame/local_frame.h"
#include "third_party/blink/renderer/core/html/canvas/canvas_rendering_context_host.h"
#include "third_party/blink/renderer/core/workers/worker_global_scope.h"
#include "third_party/blink/renderer/modules/webgl/webgl_rendering_context_base.h"

namespace {

bool AllowFingerprintingForHost(blink::CanvasRenderingContextHost* host) {
  if (!host)
    return true;
  return brave::AllowFingerprinting(host->GetTopExecutionContext(),
                                    ContentSettingsType::BRAVE_WEBCOMPAT_WEBGL);
}

}  // namespace

```

### match
```
...
 namespace blink { ...   >>> 
 ScriptObject 
 WebGLRenderingContextBase::getExtension 
 ( 
 ScriptState* script_state 
 ,  <<< ... 
const String& name
 ... ) ...  } ...  
```
### patch
```
ScriptObject WebGLRenderingContextBase::getExtension_ChromiumImpl(ScriptState* script_state,

```

### match
```
...
 namespace blink { ... 
std::optional<Vector<String>>  >>> 
 WebGLRenderingContextBase::getSupportedExtensions() 
 {  <<< ... 
if (isContextLost())
    return std::nullopt;
 ... } ...  } ...  
```
### patch
```
WebGLRenderingContextBase::getSupportedExtensions_ChromiumImpl() {

```

### match
```
...
 namespace blink { ... 
 bool WebGLRenderingContextBase::checkProgramCompletionQueryAvailable(
    WebGLProgram* program,
    bool* completed) { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```

// If fingerprinting is disallowed, claim that the only supported extension is
// WebGLDebugRendererInfo.
std::optional<Vector<String>>
WebGLRenderingContextBase::getSupportedExtensions() {
  std::optional<Vector<String>> real_extensions =
      getSupportedExtensions_ChromiumImpl();
  if (real_extensions == std::nullopt) {
    return real_extensions;
  }
  if (AllowFingerprintingForHost(Host()))
    return real_extensions;

  Vector<String> fake_extensions;
  fake_extensions.push_back(WebGLDebugRendererInfo::ExtensionName());
  return fake_extensions;
}

// If fingerprinting is disallowed and they're asking for information about any
// extension other than WebGLDebugRendererInfo, don't give it to them.
ScriptObject WebGLRenderingContextBase::getExtension(ScriptState* script_state,
                                                     const String& name) {
  if (!AllowFingerprintingForHost(Host())) {
    if (name != WebGLDebugRendererInfo::ExtensionName())
      return ScriptObject::CreateNull(v8::Isolate::GetCurrent());
  }
  return getExtension_ChromiumImpl(script_state, name);
}

```

