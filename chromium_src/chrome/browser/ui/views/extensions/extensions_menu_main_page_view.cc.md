### match
```cpp
...
 #include "base/metrics/user_metrics.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/extensions/brave_extensions_menu_entry_view.h"

```

### match
```cpp
...
 
 void ExtensionsMenuMainPageView::CreateAndInsertMenuEntry(
    ExtensionActionViewModel* action_model,
    ExtensionsMenuViewModel::MenuEntryState entry_state,
    int index) { ... 
 auto extension_id = action_model->GetId(); 
 >>> 
// base::Unretained() below is safe because `menu_handler_` lifetime is
 ... } ...  
```
### patch
```cpp
  {
    auto item = std::make_unique<BraveExtensionsMenuEntryView>(
        browser_, entry_state.is_enterprise, action_model,
        base::BindRepeating(&ExtensionsMenuHandler::OnExtensionToggleSelected,
                            base::Unretained(menu_handler_), extension_id),
        base::BindRepeating(&ExtensionsMenuHandler::OpenSitePermissionsPage,
                            base::Unretained(menu_handler_), extension_id));
    item->Update(entry_state);
    menu_entries_->AddChildViewAt(std::move(item), index);
    return;                                                                    
  }

```

