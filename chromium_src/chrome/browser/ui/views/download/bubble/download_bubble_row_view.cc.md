### match
```cpp
...
 #include "chrome/browser/ui/views/download/download_ui_context_menu_view.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/controls/hover_button.h"

```

### match
```cpp
...
 #include "ui/views/vector_icons.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "ui/views/view.h"

```

### match
```cpp
...
 } 
 // namespace 
 >>> 
 ... 
```
### patch
```cpp
constexpr auto kQuickActionAccessibilityResourceId =
    IDS_DOWNLOAD_BUBBLE_SHOW_IN_FOLDER_QUICK_ACTION_ACCESSIBILITY;


```

### match
```cpp
...
 
 DownloadBubbleRowView::DownloadBubbleRowView(
    const DownloadBubbleRowViewInfo& info,
    base::WeakPtr<DownloadBubbleUIController> bubble_controller,
    base::WeakPtr<DownloadBubbleNavigationHandler> navigation_handler,
    base::WeakPtr<Browser> browser,
    int fixed_width)
    : info_(info),
      context_menu_(std::make_unique<DownloadUiContextMenuView>(
          info_->model()->GetWeakPtr(),
          bubble_controller)),
      bubble_controller_(std::move(bubble_controller)),
      navigation_handler_(std::move(navigation_handler)),
      browser_(std::move(browser)),
      inkdrop_container_(
          AddChildView(std::make_unique<views::InkDropContainerView>())),
      update_status_text_timer_(
          FROM_HERE,
          base::Minutes(1),
          base::BindRepeating(&DownloadBubbleRowView::UpdateStatusText,
                              base::Unretained(this))),
      input_protector_(
          std::make_unique<views::InputEventActivationProtector>()),
      fixed_width_(fixed_width) { ... 
 SetNotifyEnterExitOnChild(true); 
 >>> 
// Set up initial state.
 ... } ...  
```
### patch
```cpp
  AddQuickAction(DownloadCommands::DELETE_LOCAL_FILE);

```

### match
```cpp
...
 
 case DownloadCommands : ... 
>>> 
 IDS_DOWNLOAD_BUBBLE_SHOW_IN_FOLDER_QUICK_ACTION_ACCESSIBILITY 
 , 
<<< 
...
```
### patch
```cpp
           kQuickActionAccessibilityResourceId,
    info_->model()->GetFileNameToReportUser().LossyDisplayName());
  case DownloadCommands::DELETE_LOCAL_FILE:
      return l10n_util::GetStringFUTF16(                              
         IDS_DOWNLOAD_BUBBLE_DELETE_MAIN_BUTTON_ACCESSIBILITY,

```

