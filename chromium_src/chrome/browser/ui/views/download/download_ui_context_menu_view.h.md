### match
```cpp
...
 
 class DownloadUiContextMenuView : public DownloadUiContextMenu { ... 
>>> 
 std::array<bool, DownloadCommands::kMaxValue + 1> 
<<< 
...} ...  
```
### patch
```cpp
  std::array<bool, DownloadCommands::COPY_DOWNLOAD_LINK + 1>

```

