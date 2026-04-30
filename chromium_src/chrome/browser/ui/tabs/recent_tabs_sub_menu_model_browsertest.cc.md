### match
```cpp
...
#include <utility>

 #include <vector>
 
 >>> 
#include "base/command_line.h"

 ...
```
### patch
```cpp
#include <string_view>

```

### match
```cpp
...
#include "base/command_line.h"

 #include "base/containers/span.h"
 
 >>> 
#include "base/functional/bind.h"

 ...
```
### patch
```cpp
#include "base/containers/to_vector.h"

```

### match
```cpp
...
 
 class RecentTabsSubMenuModelTest : public InProcessBrowserTest { ... 
 
 Browser* AddBrowser(Browser* browser, const GURL& url) { ... 
return new_browser;
 } 
 >>> 
 ... } ...
```
### patch
```cpp
void VerifyModel(const RecentTabsSubMenuModel& model,
                   base::span<const ModelData> data);
  void VerifyModel(const ui::MenuModel* model,
                   base::span<const ModelData> data);

```

### match
```cpp
...
 IN_PROC_BROWSER_TEST_F ( ...   >>> 
 LogMenuMetricsForShowGroupedHistory 
 ) 
 {  <<< 
Init();
 ... } ...
```
### patch
```cpp
DISABLED_LogMenuMetricsForShowGroupedHistory) {

```

### match
```cpp
...
 IN_PROC_BROWSER_TEST_F ( ...   >>> 
 RecentlyClosedTabsFromCurrentSession 
 ) 
 {  <<< 
Init();
 ...
```
### patch
```cpp
DISABLED_RecentlyClosedTabsFromCurrentSession) {

```

### match
```cpp
...
 IN_PROC_BROWSER_TEST_F ( ...   >>> 
 RecentlyClosedGroupsFromCurrentSession 
 ) 
 {  <<< 
Init();
 ...
```
### patch
```cpp
DISABLED_RecentlyClosedGroupsFromCurrentSession) {

```

### match
```cpp
...
 IN_PROC_BROWSER_TEST_F ( ...   >>> 
 RecentlyClosedTabsAndWindowsFromLastSessionWithRefresh 
 ) 
 {  <<< 
Init();
 ...
```
### patch
```cpp
DISABLED_RecentlyClosedTabsAndWindowsFromLastSessionWithRefresh) {

```

### match
```cpp
...
>>>
 IN_PROC_BROWSER_TEST_F(RecentTabsSubMenuModelTest, MaxSessionsAndRecency) 
 {  <<< 
Init();
 ... } ...  
```
### patch
```cpp
IN_PROC_BROWSER_TEST_F(RecentTabsSubMenuModelTest, DISABLED_MaxSessionsAndRecency) {

```

### match
```cpp
...
 IN_PROC_BROWSER_TEST_F ( ...   >>> 
 MaxTabsPerSessionAndRecency 
 ) 
 {  <<< 
Init();
 ... } ...  
```
### patch
```cpp
                       DISABLED_MaxTabsPerSessionAndRecency) {

```

### match
```cpp
...
IN_PROC_BROWSER_TEST_F(RecentTabsSubMenuModelTest, OtherDevicesAvailability) {
  if (!syncer::IsReplaceSyncPromosWithSignInPromosEnabled()) {
    GTEST_SKIP();
  }

  std::vector<ModelData> kDataWithOtherDevices = {
      {ui::MenuModel::TYPE_COMMAND, true},    // History
      {ui::MenuModel::TYPE_COMMAND, true},    // History Cluster
      {ui::MenuModel::TYPE_SEPARATOR, true},  // <separator>
      {ui::MenuModel::TYPE_COMMAND, false},   // Recent Tabs
      {ui::MenuModel::TYPE_SEPARATOR, true},  // <separator>
      {ui::MenuModel::TYPE_TITLE, false},     // Your devices
      {ui::MenuModel::TYPE_SUBMENU, true}     // session 0 submenu
  };

  std::vector<ModelData> kDataWithoutOtherDevices = {
      {ui::MenuModel::TYPE_COMMAND, true},    // History
      {ui::MenuModel::TYPE_COMMAND, true},    // History Cluster
      {ui::MenuModel::TYPE_SEPARATOR, true},  // <separator>
      {ui::MenuModel::TYPE_COMMAND, false}    // Recent Tabs
  };

  Init();
  EnableSync();
  RecentTabsBuilderTestHelper recent_tabs_builder;
  recent_tabs_builder.AddSession();
  recent_tabs_builder.AddWindow(0);
  recent_tabs_builder.AddTab(0, 0);
  RegisterRecentTabs(&recent_tabs_builder);

  // Default state.
  VerifyModel(RecentTabsSubMenuModel(nullptr, browser()),
              kDataWithOtherDevices);

  // Signed in.
  signin::IdentityManager* identity_manager =
      IdentityManagerFactory::GetForProfile(browser()->profile());
  signin::MakePrimaryAccountAvailable(identity_manager, "test@gmail.com",
                                      signin::ConsentLevel::kSignin);
  VerifyModel(RecentTabsSubMenuModel(nullptr, browser()),
              kDataWithOtherDevices);

  // History sync explicitly disabled: tabs from other devices are not shown.
  syncer::SyncService* sync_service =
      SyncServiceFactory::GetForProfile(browser()->profile());
  sync_service->GetUserSettings()->SetSelectedType(
      syncer::UserSelectableType::kTabs, false);
  VerifyModel(RecentTabsSubMenuModel(nullptr, browser()),
              kDataWithoutOtherDevices);
}
 #endif 
 // !BUILDFLAG(IS_CHROMEOS) 
 >>> 
 ... 
```
### patch
```cpp

// This override is in place because we must adjust the menu model to match our
// expectations
void RecentTabsSubMenuModelTest::VerifyModel(
    const RecentTabsSubMenuModel& model,
    base::span<const ModelData> input) {
  // We have to copy it over as we can not modify the input.
  auto data = base::ToVector(input);

  // We replace the "Sign in to see tabs from other devices" menu command with
  // the non-command string "No tabs from other devices" and need to adjust the
  // data
  auto& item_data = data.back();
  if (item_data.type == ui::MenuModel::TYPE_COMMAND) {
    item_data.enabled = false;
  }

  // The first two commands are History and History Clusters, but we disable
  // History Clusters and upstream won't show it, so we should skip one command.
  ::VerifyModel(model, base::span(data).subspan(1u));
}

void RecentTabsSubMenuModelTest::VerifyModel(const ui::MenuModel* model,
                                             base::span<const ModelData> data) {
  ::VerifyModel(model, data);
}
```

