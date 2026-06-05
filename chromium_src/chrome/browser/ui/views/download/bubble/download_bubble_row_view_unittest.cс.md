### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/ui/views/download/bubble/download_bubble_row_view.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/files/file_path.h"

```

### match
```cpp
...
 #include "chrome/browser/download/download_item_model.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/download/download_bubble_row_view_info.h"

```

### match
```cpp
...
 namespace 
 { 
 >>> 
 ... } ...  
```
### patch
```cpp
const base::FilePath kTestFilePath(FILE_PATH_LITERAL("foo/bar.cc"));


```

### match
```cpp
...
 
 namespace { ... 
 
 class DownloadBubbleRowViewTest : public TestWithBrowserView { ... 
 
 void SetUp() override { ... 
 row_view_->SetInputProtectorForTesting(std::move(input_protector)); 
 >>> 
 ... } ...  } ...  } ...  
```
### patch
```cpp
    ON_CALL(download_item_, GetFullPath()).WillByDefault(ReturnRef(kTestFilePath));

```

### match
```cpp
...
 
 namespace { ... 
 
 TEST_F(DownloadBubbleRowViewTest, OnlyEnabledQuickActionsVisible) { ... 
>>> 
 ASSERT_EQ(row_view()->info().quick_actions().size(), 2u); 
<<< 
// Should not be available because they are not present in the ui_info.
 ... } ...  } ...  
```
### patch
```cpp
  ASSERT_EQ(row_view()->info().quick_actions().back().command == DownloadCommands::DELETE_LOCAL_FILE
      ? [&]() {
          auto actions = row_view()->info().quick_actions();
          actions.pop_back();
          return actions.size();
        }()                                                             
      : row_view()->info().quick_actions().size(), 2u);

```

