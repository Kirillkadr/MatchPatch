### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <vector>
 
 >>> 
#include "base/functional/callback_forward.h"

 ... 
```
### patch
```cpp
#include "third_party/blink/public/mojom/clipboard/clipboard.mojom.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
void WriteImage(const SkBitmap& unsafe_bitmap) override;
 void CommitWrite() override; 
 >>> 
#if BUILDFLAG(IS_MAC)
  void WriteStringToFindPboard(const std::u16string& text) override;
  void GetPlatformPermissionState(
      GetPlatformPermissionStateCallback callback) override;
#endif
 ... } ...  
```
### patch
```cpp
  void SanitizeOnNextWriteText() override;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
// Creates a `content::ClipboardEndpoint` representing the last committed URL.
 ClipboardEndpoint CreateClipboardEndpoint(); 
 >>> 
// Stops observing clipboard changes and resets the listener.
 ... } ...  
```
### patch
```cpp
  bool sanitize_on_next_write_text_ = false;

```

