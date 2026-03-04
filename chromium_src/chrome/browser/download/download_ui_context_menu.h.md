### match
```
...
 
 # ifndef ... 
 
 class DownloadUiContextMenu : public ui::SimpleMenuModel::Delegate { ... 
// Returns the correct menu model depending on the state of the download item.
 // Returns nullptr if the download was destroyed. 
 >>> 
ui::SimpleMenuModel* GetMenuModel();
 ... } ...  
```
### patch
```
  ui::SimpleMenuModel* GetMenuModel_Chromium(); 

```

### match
```
...
 
 # ifndef ... 
// destroyed or when this object is being destroyed.
 void DetachFromDownloadItem(); 
 >>> 
ui::SimpleMenuModel* GetInProgressMenuModel(bool is_download);
 ... 
```
### patch
```
  friend class DownloadBubbleTest;

```

### match
```
...
 
 # ifndef ... 
void AddAutoOpenToMenu(ui::SimpleMenuModel* model);  >>> 
 void RecordCommandsEnabled(ui::SimpleMenuModel* model);  <<< 
// We show slightly different menus if the download is in progress vs. if the
 ... 
```
### patch
```
  void RecordCommandsEnabled(ui::SimpleMenuModel* model) {}

```

