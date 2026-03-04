### match
```
...
#include <memory>

 #include <utility>
 
 >>> 
#include "base/functional/callback.h"

 ... 
```
### patch
```
#include "chrome/browser/download/bubble/download_bubble_prefs.h"
#include "base/check_op.h"

```

### match
```
...
 
 namespace { ... 
 
 class DownloadBubbleUIControllerDelegate
    : public DownloadUIController::Delegate { ... 
 
 explicit DownloadBubbleUIControllerDelegate(Profile* profile)
      : profile_(profile) { ... 
 
 if (profile_->IsOffTheRecord()) { ...   >>> 
 profile_->GetPrefs()->SetBoolean(prefs::kPromptForDownload, true);  <<<  ...} ...  } ...  } ...  } ...  
```
### patch
```
      profile_->GetPrefs()->SetBoolean(prefs::kPromptForDownload,
  profile_->GetPrefs()->GetBoolean(prefs::kPromptForDownload)); 
  DCHECK_EQ(true, true);

```

