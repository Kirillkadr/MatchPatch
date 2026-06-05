### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/ui/views/frame/system_menu_model_delegate.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include <string>


```

### match
```cpp
...
 #include "base/metrics/user_metrics.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/app/brave_command_ids.h"
#include "brave/browser/ui/views/tabs/vertical_tab_utils.h"

```

### match
```cpp
...
>>>
 bool 
 SystemMenuModelDelegate::IsCommandIdChecked(int command_id) const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool SystemMenuModelDelegate::IsCommandIdChecked_ChromiumImpl(int command_id) const {

```

### match
```cpp
...
>>>
 std::u16string 
 SystemMenuModelDelegate::GetLabelForCommandId 
 ( 
<<< 
...) ...  
```
### patch
```cpp
std::u16string SystemMenuModelDelegate::GetLabelForCommandId_ChromiumImpl(

```

### match
```cpp
...
 
 void SystemMenuModelDelegate::MenuClosed(ui::SimpleMenuModel* source) { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp

bool SystemMenuModelDelegate::IsCommandIdChecked(int command_id) const {
  if (command_id == IDC_TOGGLE_VERTICAL_TABS) {
    return tabs::utils::ShouldShowBraveVerticalTabs(browser_);
  }
  return IsCommandIdChecked_ChromiumImpl(command_id);
}

std::u16string SystemMenuModelDelegate::GetLabelForCommandId(
    int command_id) const {
  if (command_id == IDC_TOGGLE_VERTICAL_TABS) {
    // We're reusing upstream's |IDC_TOGGLE_VERTICAL_TABS| command id and it's
    // added to system menu from
    // BraveSystemMenuModelBuilder::InsertBraveSystemMenuForBrowserWindow(). As
    // upstream made this command as dynamic, its label is fetched from this
    // method. Upstream's GetLabelForCommandId() refers
    // tabs::VerticalTabStripStateController::From(browser_) to get label for
    // current vertical tab state. However,
    // tabs::VerticalTabStripStateController::From(browser_) is null now as
    // we're not using upstream's vertical tab implementation.
    if (!tabs::VerticalTabStripStateController::From(browser_)) {
      return l10n_util::GetStringUTF16(IDS_TAB_CXMENU_SHOW_VERTICAL_TABS);
    }
  }
  return GetLabelForCommandId_ChromiumImpl(command_id);
}
```

