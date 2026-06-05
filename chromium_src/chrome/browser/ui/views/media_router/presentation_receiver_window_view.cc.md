### match
```cpp
...
 #include "base/notreached.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/brave_shields/brave_shields_web_contents_observer.h"

```

### match
```cpp
...
 
 void PresentationReceiverWindowView::Init() { ... 
 blocked_content::PopupBlockerTabHelper::CreateForWebContents(web_contents); 
 >>> 
 ... } ...  
```
### patch
```cpp
  content_settings::ageSpecificContentSettings* unused_pscs [[maybe_unused]];
  brave_shields::BraveShieldsWebContentsObserver::CreateForWebContents(
      web_contents);                                                    

```

