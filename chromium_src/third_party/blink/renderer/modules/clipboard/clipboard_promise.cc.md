### match
```
...
// found in the LICENSE file.
 #include "third_party/blink/renderer/modules/clipboard/clipboard_promise.h"
 
 >>> 
#include <memory>

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/clipboard/system_clipboard.h"

```

### match
```
...
 namespace blink { ... 
 void ClipboardPromise::HandleWriteTextWithPermission(
    mojom::blink::PermissionStatus status) { ... 
if (status != mojom::blink::PermissionStatus::GRANTED) {
    script_promise_resolver_->RejectWithDOMException(
        DOMExceptionCode::kNotAllowedError, "Write permission denied.");
    return;
  }
 SystemClipboard* system_clipboard = GetLocalFrame()->GetSystemClipboard(); 
 >>> 
system_clipboard->WritePlainText(plain_text_);
 ... } ...  } ...  
```
### patch
```
  system_clipboard->SanitizeOnNextWriteText();

```

