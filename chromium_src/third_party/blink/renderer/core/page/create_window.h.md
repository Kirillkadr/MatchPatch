### match
```
...
 # ifndef ... 
#include "third_party/blink/renderer/core/core_export.h"

 #include "third_party/blink/renderer/platform/wtf/text/wtf_string.h"
 
 >>> 
namespace blink {
class Frame;
class LocalDOMWindow;
class LocalFrame;
struct FrameLoadRequest;

Frame* CreateNewWindow(LocalFrame& opener_frame,
                       FrameLoadRequest&,
                       const AtomicString& name);

CORE_EXPORT WebWindowFeatures
GetWindowFeaturesFromString(const String& feature_string,
                            LocalDOMWindow* dom_window);

}
 ... 
```
### patch
```
#include "third_party/blink/public/web/web_window_features.h"
#include "third_party/blink/renderer/core/frame/local_dom_window.h"
#include "third_party/blink/renderer/platform/wtf/text/wtf_string.h"

```

### match
```
...
>>>
 GetWindowFeaturesFromString 
 ( 
 const String& feature_string 
 ,  <<< ... 
LocalDOMWindow* dom_window
 ... ) ...  
```
### patch
```
GetWindowFeaturesFromString_ChromiumImpl(
      const blink::String& feature_string, LocalDOMWindow* dom_window);
  CORE_EXPORT WebWindowFeatures GetWindowFeaturesFromString(const String& feature_string,

```

