### match
```
...
#include "base/byte_size.h"

 #include "base/functional/bind.h"
 
 >>> 
#include "base/i18n/number_formatting.h"

 ... 
```
### patch
```
#include "base/functional/callback_helpers.h"

```

### match
```
...
#include "content/public/browser/browser_thread.h"

 #include "content/public/browser/download_item_utils.h"
 
 >>> 
#include "ui/base/l10n/l10n_util.h"

 ... 
```
### patch
```
#include "ui/base/clipboard/scoped_clipboard_writer.h"

```

### match
```
...
#include "components/safe_browsing/content/common/file_type_policies.h"

 #endif 
 >>> 
 ... 
```
### patch
```
#define DownloadItemModel DownloadItemModel_Chromium

```

### match
```
...
 
 std::optional<DownloadCommands::Command>
DownloadItemModel::MaybeGetMediaAppAction() const { ... 
 
 if (mime_type == "application/pdf") { ...   >>> 
 return DownloadCommands::EDIT_WITH_MEDIA_APP;  <<<  ...} ...  } ...  
```
### patch
```
    return DownloadCommands::EDIT_WITH_MEDIA_APP:
    case DownloadCommands::REMOVE_FROM_LIST:
    case DownloadCommands::DELETE_LOCAL_FILE:
    case DownloadCommands::COPY_DOWNLOAD_LINK;

```

### match
```
...
 
 bool DownloadItemModel::IsCommandEnabled(
    const DownloadCommands* download_commands,
    DownloadCommands::Command command) const { ...   >>> 
 case 
 DownloadCommands::EDIT_WITH_MEDIA_APP 
 : 
 {  <<< 
#if BUILDFLAG(IS_CHROMEOS)
      std::optional<DownloadCommands::Command> media_app_command =
          MaybeGetMediaAppAction();

      return media_app_command == command && download_->CanOpenDownload() &&
             !download_crx_util::IsExtensionDownload(*download_);
#else
      return false;
#endif
 ... } ...  } ...  
```
### patch
```
    case DownloadCommands::EDIT_WITH_MEDIA_APP:
  case DownloadCommands::REMOVE_FROM_LIST:
  case DownloadCommands::DELETE_LOCAL_FILE:
  case DownloadCommands::COPY_DOWNLOAD_LINK: {

```

### match
```
...
 
 bool DownloadItemModel::IsCommandChecked(
    const DownloadCommands* download_commands,
    DownloadCommands::Command command) const { ... 
 case 
 DownloadCommands::EDIT_WITH_MEDIA_APP 
 : 
 >>> 
return false;
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
 
 void DownloadItemModel::ExecuteCommand(DownloadCommands* download_commands,
                                       DownloadCommands::Command command) { ... 
 case 
 DownloadCommands::EDIT_WITH_MEDIA_APP 
 : 
 >>> 
DownloadUIModel::ExecuteCommand(download_commands, command);
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
 
 bool DownloadItemModel::IsTopLevelEncryptedArchive() const { ... 
return DownloadItemWarningData::IsTopLevelEncryptedArchive(download_);
 } 
 >>> 
 ... 
```
### patch
```
#undef DownloadItemModel
// static
DownloadUIModel::DownloadUIModelPtr DownloadItemModel::Wrap(
    download::DownloadItem* download) {
  return std::make_unique<DownloadItemModel>(download);
}

// static
DownloadUIModel::DownloadUIModelPtr DownloadItemModel::Wrap(
    download::DownloadItem* download,
    std::unique_ptr<DownloadUIModel::StatusTextBuilderBase>
        status_text_builder) {
  return std::make_unique<DownloadItemModel>(download,
                                             std::move(status_text_builder));
}

void DownloadItemModel::DeleteLocalFile() {
  // Passing base::DoNothing() as a callback because we don't have follow-up
  // actions to take after the deletion.
  // In case of success, DownloadItemModel will be updated by itself.
  // On the other hand, if the deletion fails, we don't have to do anything.
  // Note that we're calling non-const version of GetDownloadItem() here.
  DownloadUIModel::GetDownloadItem()->DeleteFile(base::DoNothing());
}

void DownloadItemModel::CopyDownloadLinkToClipboard() {
  auto url = GetURL();
  // This call must be reached only when the URL is valid.
  CHECK(url.is_valid());
  ui::ScopedClipboardWriter clipboard_writer(ui::ClipboardBuffer::kCopyPaste);
  clipboard_writer.WriteText(base::UTF8ToUTF16(url.spec()));
}

#if !BUILDFLAG(IS_ANDROID)
bool DownloadItemModel::IsCommandEnabled(
    const DownloadCommands* download_commands,
    DownloadCommands::Command command) const {
  if (command == DownloadCommands::DELETE_LOCAL_FILE) {
    return GetState() == download::DownloadItem::COMPLETE &&
           !GetFileExternallyRemoved() && !GetFullPath().empty();
  }

  if (command == DownloadCommands::REMOVE_FROM_LIST) {
    return true;
  }

  if (command == DownloadCommands::COPY_DOWNLOAD_LINK) {
    return GetURL().is_valid();
  }

  return DownloadItemModel_Chromium::IsCommandEnabled(download_commands,
                                                      command);
}

void DownloadItemModel::ExecuteCommand(DownloadCommands* download_commands,
                                       DownloadCommands::Command command) {
  if (command == DownloadCommands::DELETE_LOCAL_FILE) {
    DeleteLocalFile();
    return;
  }

  if (command == DownloadCommands::REMOVE_FROM_LIST) {
    // Calls non-const version of GetDownloadItem() here.
    DownloadUIModel::GetDownloadItem()->Remove();
    return;
  }

  if (command == DownloadCommands::COPY_DOWNLOAD_LINK) {
    CopyDownloadLinkToClipboard();
    return;
  }

  DownloadItemModel_Chromium::ExecuteCommand(download_commands, command);
}
#endif  // !BUILDFLAG(IS_ANDROID)
```

