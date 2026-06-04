### match
```cpp
...
 #include "base/feature_list.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/frame/brave_browser_view.h"
#include "brave/browser/ui/views/frame/brave_contents_view_util.h"
#include "brave/browser/ui/views/tabs/vertical_tab_utils.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/browser_window/public/browser_window_features.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/exclusive_access/exclusive_access_manager.h"
#include "chrome/browser/ui/exclusive_access/fullscreen_controller.h"

```

### match
```cpp
...
 #include "chrome/browser/ui/views/infobars/infobar_container_view.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "chrome/browser/ui/views/side_panel/side_panel_ui.h"

```

### match
```cpp
...
 #include "chrome/common/pref_names.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "components/bookmarks/common/bookmark_pref_names.h"

```

### match
```cpp
...
 >>> 
```
### patch
```cpp
bool BrowserViewLayoutDelegateImpl::ShouldShowVerticalTabs() const {
  return browser_view().browser() &&
         tabs::utils::ShouldShowBraveVerticalTabs(browser_view().browser());
}

bool BrowserViewLayoutDelegateImpl::IsVerticalTabOnRight() const {
  return browser_view().browser() &&
         tabs::utils::IsVerticalTabOnRight(browser_view().browser());
}

bool BrowserViewLayoutDelegateImpl::
    ShouldUseBraveWebViewRoundedCornersForContents() const {
  return browser_view().browser() &&
         BraveBrowserView::ShouldUseBraveWebViewRoundedCornersForContents(
             browser_view().browser());
}

int BrowserViewLayoutDelegateImpl::GetRoundedCornersWebViewMargin() {
  return browser_view().browser()
             ? BraveContentsViewUtil::GetRoundedCornersWebViewMargin(
                   browser_view().browser())
             : 0;
}

bool BrowserViewLayoutDelegateImpl::IsBookmarkBarOnByPref() const {
  return browser_view().browser() &&
         browser_view().browser()->profile()->GetPrefs()->GetBoolean(
             bookmarks::prefs::kShowBookmarkBar);
}

bool BrowserViewLayoutDelegateImpl::IsContentTypeSidePanelVisible() {
  if (!browser_view().browser()) {
    return false;
  }

  return browser_view()
      .browser()
      ->GetFeatures()
      .side_panel_ui()
      ->GetCurrentEntryId(SidePanelEntry::PanelType::kContent)
      .has_value();
}

bool BrowserViewLayoutDelegateImpl::IsFullscreenForBrowser() {
  if (!browser_view().browser()) {
    return false;
  }
  ExclusiveAccessManager* exclusive_access_manager =
      browser_view().browser()->GetFeatures().exclusive_access_manager();
  if (!exclusive_access_manager) {
    return false;
  }
  auto* fullscreen_controller =
      exclusive_access_manager->fullscreen_controller();
  return fullscreen_controller &&
         fullscreen_controller->IsFullscreenForBrowser();
}

bool BrowserViewLayoutDelegateImpl::IsFullscreenForTab() const {
  if (!browser_view().browser()) {
    return false;
  }
  const ExclusiveAccessManager* exclusive_access_manager =
      browser_view().browser()->GetFeatures().exclusive_access_manager();
  if (!exclusive_access_manager) {
    return false;
  }
  const auto* fullscreen_controller =
      exclusive_access_manager->fullscreen_controller();
  return fullscreen_controller &&
         fullscreen_controller->IsWindowFullscreenForTabOrPending();
}

bool BrowserViewLayoutDelegateImpl::IsFullscreen() const {
  return browser_view().IsFullscreen();
}
```

