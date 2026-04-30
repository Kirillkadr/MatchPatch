### match
```cpp
...
#include "base/test/bind.h"

 #include "base/test/scoped_feature_list.h"
 
 >>> 
#include "chrome/browser/download/download_item_model.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/download/download_commands.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 TEST_F(DownloadBubbleRowViewInfoTest, InProgressOrCompletedInfo) { ... 
 
 EXPECT_THAT ( ... 
 
 UnorderedElementsAre ( ...   >>> 
 DownloadCommands::Command::OPEN_WHEN_COMPLETE 
 ) 
 ) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
                           DownloadCommands::Command::OPEN_WHEN_COMPLETE, DownloadCommands::Command::DELETE_LOCAL_FILE));

```

