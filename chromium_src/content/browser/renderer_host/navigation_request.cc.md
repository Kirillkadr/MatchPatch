### match
```cpp
...
#include <utility>

 #include <vector>
 
 >>> 
#include "base/auto_reset.h"

 ... 
```
### patch
```cpp
#include "build/build_config.h"
#include "content/browser/renderer_host/frame_tree.h"
#include "content/browser/renderer_host/frame_tree_node.h"
#include "url/gurl.h"
#if BUILDFLAG(IS_ANDROID)
#include "content/browser/renderer_host/navigator.h"
#include "content/public/browser/navigation_controller.h"
#include "content/public/browser/navigation_entry.h"
#endif

```

### match
```cpp
...
#include "ui/android/window_android_compositor.h"

 #endif 
 >>> 
 ... 
```
### patch
```cpp
namespace {

GURL GetTopDocumentGURL(content::FrameTreeNode* frame_tree_node) {
  GURL gurl;
#if BUILDFLAG(IS_ANDROID)
  // On Android, a base URL can be set for the frame. If this the case, it is
  // the URL to use for cookies.
  content::NavigationEntry* last_committed_entry =
      frame_tree_node->navigator().controller().GetLastCommittedEntry();
  if (last_committed_entry)
    gurl = last_committed_entry->GetBaseURLForDataURL();
#endif
  if (gurl.is_empty())
    gurl = frame_tree_node->frame_tree().root()->current_url();
  return gurl;
}

}  // namespace

```

