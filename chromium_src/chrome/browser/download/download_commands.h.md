### match
```
...
 
 # ifndef ... 
 
 class DownloadCommands { ... 
 
 enum Command { ... 
// Bypass the prompt to deep scan and
 // open the file. 
 >>> 
OPEN_WITH_MEDIA_APP = 21
 ... } ...  } ...  
```
### patch
```
    /* Removes the download item from the list. The actual file is not */
  /* deleted. Used by download shelf view. */
  REMOVE_FROM_LIST = 23,
  /* Remove downloaded file from disk and and remove the download item from */
  /* the list. Used by download bubble view. */
  DELETE_LOCAL_FILE = 24,
  /* Copy download link to clipboard from DownloadUIContextMenuView */
  COPY_DOWNLOAD_LINK = 25,

```

### match
```
...
 #endif 
 // CHROME_BROWSER_DOWNLOAD_DOWNLOAD_COMMANDS_H_ 
 >>> 
 ... 
```
### patch
```

static_assert(DownloadCommands::Command::kMaxValue ==
                  DownloadCommands::Command::EDIT_WITH_MEDIA_APP,
              "We should update kRemoveFromList and kDeleteLocalFile values if "
              "we change the max value of DownloadCommands::Command");
```

