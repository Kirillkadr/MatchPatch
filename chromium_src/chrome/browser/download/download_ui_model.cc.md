### match
```
...
 
 bool DownloadUIModel::IsCommandEnabled(
    const DownloadCommands* download_commands,
    DownloadCommands::Command command) const { ... 
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
 
 bool DownloadUIModel::IsCommandChecked(
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
 
 void DownloadUIModel::ExecuteCommand(DownloadCommands* download_commands,
                                     DownloadCommands::Command command) { ... 
case DownloadCommands::OPEN_WITH_MEDIA_APP:
 case DownloadCommands::EDIT_WITH_MEDIA_APP: 
 >>> 
#if BUILDFLAG(IS_CHROMEOS)
      OpenUsingMediaApp();
      break;
#else
      NOTREACHED();
#endif
 ... } ...  
```
### patch
```
    case DownloadCommands::REMOVE_FROM_LIST:
    case DownloadCommands::DELETE_LOCAL_FILE:
    case DownloadCommands::COPY_DOWNLOAD_LINK:

```

