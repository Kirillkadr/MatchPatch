### match
```
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "third_party/blink/renderer/core/frame/dom_window.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/frame/dom_window.h"

```

### match
```
...
 namespace blink { ... 
 void DOMWindow::DisconnectCoopAccessMonitor(
    const LocalFrameToken& accessing_main_frame) { ... 
EraseIf(coop_access_monitor_,
          [&accessing_main_frame](const Member<CoopAccessMonitor>& monitor) {
            return monitor->accessing_main_frame == accessing_main_frame;
          });
 } 
 >>> 
 ... } ...  
```
### patch
```
LocalFrame* DOMWindow::GetDisconnectedFrame() const {
  // IncumbentDOMWindow is safe to call only when an active v8 context is
  // present.
  if (auto* isolate = v8::Isolate::TryGetCurrent();
      !isolate || !isolate->InContext()) {
    return nullptr;
  }

  v8::Isolate* isolate = v8::Isolate::GetCurrent();
  LocalDOMWindow* accessing_window = IncumbentDOMWindow(isolate);
  LocalFrame* accessing_frame = accessing_window->GetFrame();
  return accessing_frame;
}

```

