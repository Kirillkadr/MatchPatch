### match
```cpp
...
 
 void DownloadUiContextMenuView::ExecuteCommand(int command_id,
                                               int event_flags) { ... 
 
 if (!download_commands_executed_recorded_[command_id]) { ... 
>>> 
 base::UmaHistogramEnumeration(
        "Download.ContextMenuAction",
        DownloadCommandToContextMenuAction(
            static_cast<DownloadCommands::Command>(command_id),
            /*clicked=*/true)); 
<<< 
...} ...  } ...  
```
### patch
```cpp

```

