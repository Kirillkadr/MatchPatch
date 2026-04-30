### match
```cpp
...
#include <memory>

 #include <set>
 
 >>> 
#include "base/containers/fixed_flat_set.h"

 ...
```
### patch
```cpp
#include "base/check.h"

```

### match
```cpp
...
#include "base/strings/string_util.h"

 #include "base/strings/utf_string_conversions.h"
 
 >>> 
#include "build/build_config.h"

 ...
```
### patch
```cpp
#include "brave/browser/ui/toolbar/brave_recent_tabs_sub_menu_model.h"

```

### match
```cpp
...
#include "chrome/browser/ui/browser_window/public/browser_window_features.h"

 #include "chrome/browser/ui/side_panel/side_panel_ui.h"
 
 >>> 
#include "chrome/browser/ui/tabs/tab_group_theme.h"

 ...
```
### patch
```cpp
#include "chrome/browser/ui/singleton_tabs.h"

```

### match
```cpp
...
 
 namespace { ... 
 AppMenuModel::kNumUnboundedMenuTypes 
 ; 
 >>> 
 ... } ...
```
### patch
```cpp
constexpr char kBraveStubSessionTag[] = "brave_stub_more_session_tag";
constexpr char kBraveSyncedTabsUrl[] = "brave://history/syncedTabs";

```

### match
```cpp
...
if (!open_tabs || !open_tabs->GetAllForeignSessions(&sessions)) {
 
 >>> ...
  <<<  } ...
```
### patch
```cpp
AddItemWithStringId(IDC_RECENT_TABS_NO_DEVICE_TABS,
                        IDS_RECENT_TABS_NO_DEVICE_TABS);

```

### match
```cpp
...
 
 if (!open_tabs || !open_tabs->GetAllForeignSessions(&sessions)) { ... 
 IDS_RECENT_TABS_NO_DEVICE_TABS 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  }



```

### match
```cpp
...
 
 void RecentTabsSubMenuModel::BuildTabsFromOtherDevices() { ... 
 
 for (size_t i = 0;
       i < sessions.size() && num_sessions_added < kMaxSessionsToShow; ++i) { ... 
 CreateOtherDeviceSubMenu(session, tabs_in_session) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp

    if (tabs_in_session.size() > kMaxSessionsToShow) {
    /* Not all the tabs are shown in menu */
    if (!stub_tab_.get()) {
      stub_tab_.reset(new sessions::SessionTab());
      sessions::SerializedNavigationEntry stub_nav_entry;
      stub_nav_entry.set_title(
          l10n_util::GetStringUTF16(IDS_OPEN_MORE_OTHER_DEVICES_SESSIONS));
      stub_nav_entry.set_virtual_url(GURL(kBraveSyncedTabsUrl));
      stub_tab_->navigations.push_back(stub_nav_entry);
      stub_tab_->tab_id = SessionID::NewUnique();
    }
    tabs_in_session[kMaxSessionsToShow] = stub_tab_.get();
    BuildOtherDevicesTabItem(device_menu_model.get(), kBraveStubSessionTag,
                             *tabs_in_session[kMaxSessionsToShow]);
  }

```

### match
```cpp
...
 
 bool RecentTabsSubMenuModel::IsCommandType(CommandType command_type,
                                           int command_id) const { ... 
NOTREACHED();
 } 
 >>> 
 ... 
```
### patch
```cpp

BraveRecentTabsSubMenuModel::BraveRecentTabsSubMenuModel(
    ui::AcceleratorProvider* accelerator_provider,
    Browser* browser)
    : RecentTabsSubMenuModel(accelerator_provider, browser) {}

BraveRecentTabsSubMenuModel::~BraveRecentTabsSubMenuModel() {}

void BraveRecentTabsSubMenuModel::ExecuteCommand(int command_id,
                                                 int event_flags) {
  if (IsCommandType(CommandType::Tab, command_id)) {
    const TabItems& tab_items = *GetTabVectorForCommandId(command_id);
    const TabItem& item = tab_items.at(command_id);
    DCHECK(item.tab_id.is_valid() && item.url.is_valid());

    if (item.session_tag == kBraveStubSessionTag) {
      ShowSingletonTabOverwritingNTP(browser_, GURL(kBraveSyncedTabsUrl));
      return;
    }
  }

  if (command_id == IDC_CLEAR_BROWSING_DATA) {
    chrome::ExecuteCommand(browser_, command_id);
    return;
  }

  RecentTabsSubMenuModel::ExecuteCommand(command_id, event_flags);
}
```

