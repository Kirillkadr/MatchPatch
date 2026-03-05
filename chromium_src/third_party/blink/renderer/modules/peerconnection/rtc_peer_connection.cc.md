### match
```
...
#include <string>

 #include <utility>
 
 >>> 
#include "base/compiler_specific.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/messaging/message_port.h"
#include "third_party/blink/renderer/platform/instrumentation/instance_counters.h"
#include "third_party/blink/renderer/platform/runtime_enabled_features.h"

```

### match
```
... 
if (RuntimeEnabledFeatures::
          FencedFramesLocalUnpartitionedDataAccessEnabled() &&
      window->GetFrame()->IsInFencedFrameTree()) {
    exception_state.ThrowDOMException(
        DOMExceptionCode::kNotAllowedError,
        "RTCPeerConnection is not allowed in fenced frames.");
    return;
  }

  InstanceCounters::IncrementCounter(
      InstanceCounters::kRTCPeerConnectionCounter);
 >>>  ...
```
### patch
```
      if (RuntimeEnabledFeatures::BraveIsInTorContextEnabled()) {              \
    exception_state.ThrowDOMException(DOMExceptionCode::kNotAllowedError,  \
                                      "RTCPeerConnection is not allowed"); \
    return;                                                                \
  }

```

