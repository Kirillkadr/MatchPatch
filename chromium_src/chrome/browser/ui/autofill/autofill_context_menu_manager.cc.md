### match
```cpp
...
#include <algorithm>

 #include <string>
 
 >>> 
#include "base/containers/fixed_flat_set.h"

 ... 
```
### patch
```cpp
#include "base/check_op.h"

```

### match
```cpp
...
 
 namespace autofill { ...   >>> 
 void 
 AutofillContextMenuManager::AppendItems() 
 {  <<< 
if (params_.is_content_editable_for_autofill) {
    MaybeAddAutofillAtMemoryItem();
    return;
  }
 ... } ...  } ...  
```
### patch
```cpp
void AutofillContextMenuManager::AppendItems_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace autofill { ... 
 
 void AutofillContextMenuManager::MaybeMarkLastItemAsNewFeature(
    const base::Feature& feature) { ... 
menu_model_->SetIsNewFeatureAt(menu_model_->GetItemCount() - 1,
                                 UserEducationService::MaybeShowNewBadge(
                                     delegate_->GetBrowserContext(), feature));
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void AutofillContextMenuManager::AppendItems() {
  AppendItems_ChromiumImpl();

  // Remove feedback menu item if present (and the separator that comes after
  // it).
  const std::optional<size_t> feedback_item_index =
      menu_model_->GetIndexOfCommandId(IDC_CONTENT_CONTEXT_AUTOFILL_FEEDBACK);
  if (feedback_item_index.has_value()) {
    menu_model_->RemoveItemAt(feedback_item_index.value());
    DCHECK_EQ(ui::MenuModel::TYPE_SEPARATOR,
              menu_model_->GetTypeAt(feedback_item_index.value()));
    menu_model_->RemoveItemAt(feedback_item_index.value());
  }
}


```

