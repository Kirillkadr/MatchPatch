### match
```
...
#include "chrome/browser/download/bubble/download_display_controller.h"

 #include "chrome/browser/download/chrome_download_manager_delegate.h"
 
 >>> 
#include "chrome/browser/download/download_core_service.h"

 ... 
```
### patch
```
#include "chrome/browser/download/download_commands.h"

```

### match
```
...
 
 void DownloadBubbleUIController::ProcessDownloadButtonPress(
    base::WeakPtr<DownloadUIModel> model,
    DownloadCommands::Command command,
    bool is_main_view) { ... 
DownloadCommands commands(model);  >>> 
 base::UmaHistogramEnumeration("Download.Bubble.ProcessedCommand2", command);  <<< 
DownloadItemWarningData::WarningSurface warning_surface =
      is_main_view ? DownloadItemWarningData::WarningSurface::BUBBLE_MAINPAGE
                   : DownloadItemWarningData::WarningSurface::BUBBLE_SUBPAGE;
 ... } ...  
```
### patch
```

```

### match
```
...
 
 void DownloadBubbleUIController::ProcessDownloadButtonPress(
    base::WeakPtr<DownloadUIModel> model,
    DownloadCommands::Command command,
    bool is_main_view) { ... 
 case 
 DownloadCommands::OPEN_SAFE_BROWSING_SETTING 
 : 
 >>> 
commands.ExecuteCommand(command);
 ... } ...  
```
### patch
```
    case DownloadCommands::DELETE_LOCAL_FILE:

```

