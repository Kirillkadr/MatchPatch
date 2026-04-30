### match
```cpp
...
#include "chrome/browser/ui/tabs/vertical_tab_strip_state_controller.h"

 #include "chrome/browser/ui/thumbnails/thumbnail_tab_helper.h"
 
 >>> 
#include "chrome/browser/ui/ui_features.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/tabs/dragging/tab_drag_controller.h"

```

### match
```cpp
...
 
 void TabStripModel::ExecuteContextMenuCommand(int context_index,
                                              ContextMenuCommand command_id) { ... 
case CommandFirst:
 case CommandAddNote: 
 >>> 
case CommandLast:
      NOTREACHED();
 ... } ...  
```
### patch
```cpp
    case CommandRestoreTab:
    case CommandBookmarkAllTabs:
    case CommandShowVerticalTabs:
    case CommandToggleTabMuted:
    case CommandBringAllTabsToThisWindow:
    case CommandCloseDuplicateTabs:
    case CommandOpenInContainer:
    case CommandRenameTab:

```

### match
```cpp
...
 std::pair<std::optional<int>, std::optional<int>>
TabStripModel::GetAdjacentTabsAfterSelectedMove ( ...   >>> 
 base::PassKey<DraggingTabsSession> 
 ,  <<< 
int destination_index
 ... ) ...  
```
### patch
```cpp
    base::PassKey<DraggingTabsSessionChromium>,

```

### match
```cpp
...
 
 void TabStripModel::InsertTabAtIndexImpl(
    std::unique_ptr<tabs::TabModel> tab_model,
    int index,
    std::optional<tab_groups::TabGroupId> group,
    bool pin,
    bool active) { ... 
tabs::TabInterface* old_active_tab = GetActiveTab();  >>> 
 contents_data_->AddTabRecursive(std::move(tab_model), index, group, pin);  <<< 
selection_model_.InvalidateListSelectionModel(base::PassKey<TabStripModel>());
 ... } ...  
```
### patch
```cpp
  contents_data_->  /* meaningless call to address "contents_data_->" */
  pinned_collection();
  auto* opener = tab_model->opener();
  contents_data_->AddTabRecursive(std::move(tab_model), index, group, pin, opener);

```

