### match
```
...
#include "base/notreached.h"

 #include "build/build_config.h"
 
 >>> 
#include "chrome/browser/download/download_ui_model.h"

 ... 
```
### patch
```
#include "chrome/browser/download/download_commands.h"

```

### match
```
...
 
 DownloadUiContextMenuAction DownloadCommandToContextMenuAction(
    DownloadCommands::Command download_command,
    bool clicked) { ... 
 case 
 DownloadCommands::Command::EDIT_WITH_MEDIA_APP 
 : 
 >>> 
NOTREACHED();
 ... } ...  
```
### patch
```
    case DownloadCommands::REMOVE_FROM_LIST:
    case DownloadCommands::DELETE_LOCAL_FILE:
    case DownloadCommands::COPY_DOWNLOAD_LINK:

```

