### match
```
...
 
 bool OfflineItemModel::IsCommandEnabled(
    const DownloadCommands* download_commands,
    DownloadCommands::Command command) const { ... 
 case 
 DownloadCommands::EDIT_WITH_MEDIA_APP 
 : 
 >>> 
NOTIMPLEMENTED();
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
 
 bool OfflineItemModel::IsCommandChecked(
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
 
 void OfflineItemModel::ExecuteCommand(DownloadCommands* download_commands,
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

