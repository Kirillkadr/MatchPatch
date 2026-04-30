### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/ui/download/download_bubble_info_utils.h"
 
 >>> 
#include "chrome/app/vector_icons/vector_icons.h"

 ... 
```
### patch
```cpp
#include "brave/components/vector_icons/vector_icons.h"

```

### match
```cpp
...
#include "brave/components/vector_icons/vector_icons.h"

 #include "chrome/app/vector_icons/vector_icons.h"
 
 >>> 
#include "chrome/browser/download/download_ui_model.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/download/download_commands.h"

```

### match
```cpp
...
 
 std::vector<DownloadBubbleQuickAction> QuickActionsForDownload(
    const DownloadUIModel& model) { ... 
 
 else { ... 
 
 actions.emplace_back ( ... 
 &vector_icons::kLaunchChromeRefreshIcon 
 ) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  actions.emplace_back<DownloadCommands::Command>(
      DownloadCommands::Command(DownloadCommands::DELETE_LOCAL_FILE),
      l10n_util::GetStringUTF16(IDS_DOWNLOAD_BUBBLE_DELETE),   
      &kLeoTrashIcon);

```

