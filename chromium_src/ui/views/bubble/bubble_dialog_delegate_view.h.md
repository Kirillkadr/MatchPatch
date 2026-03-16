### match
```cpp

...
#include "ui/base/cocoa/bubble_closer.h"

 #endif 
 >>> 
 ... 
```
### patch
```cpp

class BraveNewsBubbleView;
class BraveHelpBubbleDelegateView;
class SplitViewMenuBubble;
class WaybackMachineBubbleView;
class SidebarItemAddedFeedbackBubble;
class SidebarEditItemBubbleDelegateView;
class SidebarAddItemBubbleDelegateView;

```

### match
```cpp

...
 # ifndef ... 
 namespace ambient_signin { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp

namespace playlist {
class PlaylistBubbleView;
}  // namespace playlist

```

### match
```cpp

...
 # ifndef ... 
 namespace 
 views 
 { 
 >>> 
class AnchorTestBubbleDialogDelegateView
 ... } ...  
```
### patch
```cpp

class BraveBubbleDialogDelegateView;

```

### match
```cpp

...
 # ifndef ... 
 bool autosize = false 
 ) 
 ; 
 >>> 
static BddvPassKey CreatePassKey() { return BddvPassKey(); }
 ... 
```
### patch
```cpp

  friend class ::BraveNewsBubbleView;
  friend class ::BraveHelpBubbleDelegateView;
  friend class ::WaybackMachineBubbleView;
  friend class ::playlist::PlaylistBubbleView;
  friend class ::SplitViewMenuBubble;
  friend class ::SidebarItemAddedFeedbackBubble;
  friend class ::SidebarEditItemBubbleDelegateView;
  friend class ::SidebarAddItemBubbleDelegateView;
  friend class ::views::BraveBubbleDialogDelegateView; 

```

