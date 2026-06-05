### match
```cpp
...
#include "base/command_line.h"

 #include "base/feature_list.h"
 
 >>> 
#include "base/functional/bind.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 std::unique_ptr<DesktopMediaPicker> DesktopMediaPicker::Create(
    const content::MediaStreamRequest* request) { ... 
if (request &&
      request->video_type ==
          blink::mojom::MediaStreamType::DISPLAY_VIDEO_CAPTURE_THIS_TAB) {
    return std::make_unique<ShareThisTabMediaPicker>();
  } else {
    return std::make_unique<DesktopMediaPickerImpl>();
  }
 } 
 >>> 
 ... 
```
### patch
```cpp

// Upstream enabled this feature via finch field trial. We need this feature
// enabled as well as it addresses a security exploit.
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kDesktopMediaPickerMultiLineTitle, base::FEATURE_ENABLED_BY_DEFAULT},
}});
```

