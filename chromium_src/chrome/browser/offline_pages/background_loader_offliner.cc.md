### match
```cpp
...
#include "base/task/single_thread_task_runner.h"

 #include "base/time/time.h"
 
 >>> 
#include "chrome/browser/content_settings/page_specific_content_settings_delegate.h"

 ... 
```
### patch
```cpp
#include "brave/browser/brave_shields/brave_shields_web_contents_observer.h"

```

### match
```cpp
...
 
 namespace offline_pages { ... 
 
 void BackgroundLoaderOffliner::ResetLoader() { ... 
 
 renderer_preferences_util::UpdateFromSystemSettings ( ... 
 Profile::FromBrowserContext(browser_context_) 
 ) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  content_settings::PageSpecificContentSettings* unused_pscs [[maybe_unused]];
  brave_shields::BraveShieldsWebContentsObserver::CreateForWebContents(
      loader_->web_contents());

```

