### match
```
...
#include "chrome/browser/download/download_commands.h"

 #include "chrome/browser/download/download_stats.h"
 
 >>> 
#include "chrome/grit/generated_resources.h"

 ... 
```
### patch
```
#include "chrome/browser/download/download_ui_model.h"

```

### match
```
...
#include "ui/gfx/color_palette.h"

 #include "ui/menus/simple_menu_model.h"
 
 >>> 
using InsecureDownloadStatus = download::DownloadItem::InsecureDownloadStatus;
 ... 
```
### patch
```
namespace {

bool AlreadyHasCommand(int command_id, ui::SimpleMenuModel* model) {
  return model && model->GetIndexOfCommandId(command_id).has_value();
}

void MaybeAddRemoveFromListCommand(DownloadUIModel& download,
                                   ui::SimpleMenuModel* model) {
  // Early return if |model| has the item. |model| is cached by base class.
  if (AlreadyHasCommand(DownloadCommands::REMOVE_FROM_LIST, model)) {
    return;
  }

  // Don't add "Remove item fro list" entry to in-progress state.
  if (download.GetState() != download::DownloadItem::COMPLETE &&
      download.GetState() != download::DownloadItem::CANCELLED) {
    return;
  }

  if (auto index =
          model->GetIndexOfCommandId(DownloadCommands::SHOW_IN_FOLDER)) {
    model->InsertItemAt(
        *index + 1, DownloadCommands::REMOVE_FROM_LIST,
        l10n_util::GetStringUTF16(IDS_DOWNLOAD_DELETE_FROM_HISTORY));
  }
}

void MaybeAddCopyDownloadLinkMenuItem(DownloadUIModel& download,
                                      ui::SimpleMenuModel* model) {
  // Early return if |model| has the item. |model| is cached by base class.
  if (AlreadyHasCommand(DownloadCommands::COPY_DOWNLOAD_LINK, model)) {
    return;
  }

  if (auto index =
          model->GetIndexOfCommandId(DownloadCommands::SHOW_IN_FOLDER)) {
    model->InsertItemAt(
        *index + 1, DownloadCommands::COPY_DOWNLOAD_LINK,
        l10n_util::GetStringUTF16(IDS_DOWNLOAD_COPY_DOWNLOAD_LINK));
  }
}

void InsertBraveSpecificCommandsToModel(
    const base::WeakPtr<DownloadUIModel>& download,
    ui::SimpleMenuModel* model) {
  if (!download) {
    return;
  }

  MaybeAddCopyDownloadLinkMenuItem(*download, model);
  MaybeAddRemoveFromListCommand(*download, model);
}

}  // namespace


```

### match
```
...
DownloadUiContextMenu::DownloadUiContextMenu(
    base::WeakPtr<DownloadUIModel> download)
    : download_(download), download_commands_(new DownloadCommands(download)) {
  DCHECK(download_);
}  >>> 
 void DownloadUiContextMenu::RecordCommandsEnabled(ui::SimpleMenuModel* model) {
  // Meant to be kept up-to-date with DownloadCommands::Command

  if (download_commands_enabled_recorded_) {
    return;
  }

  for (int command_int = 0; command_int <= DownloadCommands::Command::kMaxValue;
       command_int++) {
    if (model->GetIndexOfCommandId(command_int).has_value() &&
        IsCommandIdEnabled(command_int)) {
      DownloadCommands::Command download_command =
          static_cast<DownloadCommands::Command>(command_int);
      base::UmaHistogramEnumeration(
          "Download.ContextMenuAction",
          DownloadCommandToContextMenuAction(download_command,
                                             /*clicked=*/false));
    }
  }

  download_commands_enabled_recorded_ = true;
} 
 ui::SimpleMenuModel 
 * DownloadUiContextMenu::GetMenuModel() 
 {  <<< 
ui::SimpleMenuModel* model = nullptr;
 ... } ...  
```
### patch
```
ui::SimpleMenuModel* DownloadUiContextMenu::GetMenuModel_Chromium() {

```

### match
```
...
 
 DownloadUiContextMenu::DownloadUiContextMenu(
    base::WeakPtr<DownloadUIModel> download)
    : download_(download), download_commands_(new DownloadCommands(download)) { ... 
DCHECK(download_);
 } 
 >>> 
 ... 
```
### patch
```



```

### match
```
...
 
 std::u16string DownloadUiContextMenu::GetLabelForCommandId(
    int command_id) const { ... 
 case 
 DownloadCommands::EDIT_WITH_MEDIA_APP 
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

### match
```
...
 
 void DownloadUiContextMenu::AddAutoOpenToMenu(ui::SimpleMenuModel* menu) { ... 
if (download_->IsOpenWhenCompleteByPolicy()) {
    menu->AddItemWithIcon(
        DownloadCommands::ALWAYS_OPEN_TYPE,
        GetLabelForCommandId(DownloadCommands::ALWAYS_OPEN_TYPE),
        ui::ImageModel::FromVectorIcon(vector_icons::kBusinessIcon,
                                       ui::kColorIcon,
                                       ui::SimpleMenuModel::kDefaultIconSize));
  } else {
    menu->AddCheckItem(
        DownloadCommands::ALWAYS_OPEN_TYPE,
        GetLabelForCommandId(DownloadCommands::ALWAYS_OPEN_TYPE));
  }
 } 
 >>> 
 ... 
```
### patch
```

ui::SimpleMenuModel* DownloadUiContextMenu::GetMenuModel() {
  auto* model = GetMenuModel_Chromium();
  InsertBraveSpecificCommandsToModel(download_, model);
  return model;
}
```

