### match
```
...
 # ifndef ... 
#define THIRD_PARTY_BLINK_RENDERER_CORE_PAGE_CHROME_CLIENT_H_

 #include <memory>
 
 >>> 
#include "base/functional/callback.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/platform/graphics/dom_node_id.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT ChromeClient : public GarbageCollected<ChromeClient> { ... 
virtual bool TabsToLinks() = 0;
 virtual const display::ScreenInfo& GetScreenInfo(LocalFrame& frame) const = 0; 
 >>> 
virtual const display::ScreenInfos& GetScreenInfos(
      LocalFrame& frame) const = 0;
 ... } ...  } ...  
```
### patch
```
  virtual const display::ScreenInfos& BraveGetScreenInfos(LocalFrame& frame) const;  \
  virtual DOMNodeId InitiatorDomNodeId() const {
    return kInvalidDOMNodeId;
  }

```

