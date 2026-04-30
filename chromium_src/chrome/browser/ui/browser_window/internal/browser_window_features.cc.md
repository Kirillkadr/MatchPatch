### match
```cpp
...
#include "base/memory/ptr_util.h"

 #include "base/no_destructor.h"
 
 >>> 
#include "chrome/browser/actor/ui/actor_border_view_controller.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/brave_browser_actions.h"
#include "brave/browser/ui/brave_browser_command_controller.h"
#include "brave/browser/ui/brave_browser_content_setting_bubble_model_delegate.h"
#include "brave/browser/ui/toolbar/brave_location_bar_model_delegate.h"
#include "brave/browser/ui/views/side_panel/bookmarks/brave_bookmarks_side_panel_coordinator.h"
#include "brave/browser/ui/views/side_panel/brave_side_panel_coordinator.h"

```

### match
```cpp
...
// namespace  >>> 
 BrowserWindowFeatures::BrowserWindowFeatures() = default; 
 BrowserWindowFeatures::~BrowserWindowFeatures() = default;  <<< 
 ... 
```
### patch
```cpp
BrowserWindowFeatures_ChromiumImpl::BrowserWindowFeatures_ChromiumImpl() = default;
BrowserWindowFeatures_ChromiumImpl::~BrowserWindowFeatures_ChromiumImpl() = default;

```

### match
```cpp
...
>>>
 void 
 BrowserWindowFeatures::Init(BrowserWindowInterface* browser) 
 {  <<< 
// This is used only for the controllers which will be created on demand
 ... } ...  
```
### patch
```cpp

void BrowserWindowFeatures_ChromiumImpl::Init(BrowserWindowInterface* browser) {

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::Init(BrowserWindowInterface* browser) { ... 
app_browser_controller_ =
      GetUserDataFactory().CreateInstanceWithFactoryMethod(
          *browser, &web_app::MaybeCreateAppBrowserController, browser);  >>> 
 browser_actions_ = std::make_unique<BrowserActions>(browser);  <<< 
browser_command_controller_ =
      std::make_unique<chrome::BrowserCommandController>(browser);
 ... } ...  
```
### patch
```cpp
  browser_actions_ = std::make_unique<BraveBrowserActions>(browser);

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::Init(BrowserWindowInterface* browser) { ...   >>> 
 std::make_unique<chrome::BrowserCommandController>(browser) 
 ;  <<<  ...} ...  
```
### patch
```cpp
      std::make_unique<chrome::BraveBrowserCommandController>(browser);

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::Init(BrowserWindowInterface* browser) { ...   >>> 
 std::make_unique<BrowserLocationBarModelDelegate>(tab_strip_model_) 
 ;  <<<  ...} ...  
```
### patch
```cpp
      std::make_unique<BraveLocationBarModelDelegate>(tab_strip_model_);

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::Init(BrowserWindowInterface* browser) { ...   >>> 
 GetUserDataFactory().CreateInstance<BookmarksSidePanelCoordinator> 
 (  <<< 
*browser
 ... ) ...  } ...  
```
### patch
```cpp
      GetUserDataFactory().CreateInstance<BraveBookmarksSidePanelCoordinator>(

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::Init(BrowserWindowInterface* browser) { ...   >>> 
 std::make_unique<BrowserContentSettingBubbleModelDelegate>(browser) 
 ;  <<<  ...} ...  
```
### patch
```cpp
      std::make_unique<BraveBrowserContentSettingBubbleModelDelegate>(browser);

```

### match
```cpp
...
>>>
 void 
 BrowserWindowFeatures::InitPostWindowConstruction(Browser* browser) 
 {  <<< 
desktop_browser_window_capabilities_ =
      GetUserDataFactory().CreateInstance<DesktopBrowserWindowCapabilities>(
          *browser, browser, browser->window(),
          browser->GetUnownedUserDataHost());
 ... } ...  
```
### patch
```cpp
void BrowserWindowFeatures_ChromiumImpl::InitPostWindowConstruction(Browser* browser) {

```

### match
```cpp
...
>>>
 void 
 BrowserWindowFeatures::InitPostBrowserViewConstruction 
 (  <<< 
BrowserView* browser_view
 ... ) ...  
```
### patch
```cpp
void BrowserWindowFeatures_ChromiumImpl::InitPostBrowserViewConstruction(

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::InitPostBrowserViewConstruction(
BrowserView* browser_view) { ... 
browser_animation_controller_->AddAnimationProvider(
      std::make_unique<TabStripAnimations>());  >>> 
 // TODO(crbug.com/346148093): Move SidePanelCoordinator construction to  <<< 
// Init.
 ... } ...  
```
### patch
```cpp
  // TODO(crbug.com/346148093): Move BraveSidePanelCoordinator construction to

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::InitPostBrowserViewConstruction(
BrowserView* browser_view) { ... 
// Init.  >>> 
 // TODO(crbug.com/346148554): Do not create a SidePanelCoordinator for most  <<< 
// browser.h types
 ... } ...  
```
### patch
```cpp
  // TODO(crbug.com/346148554): Do not create a BraveSidePanelCoordinator for most

```

### match
```cpp
...
 
 void BrowserWindowFeatures_ChromiumImpl::InitPostBrowserViewConstruction(
BrowserView* browser_view) { ...   >>> 
 GetUserDataFactory().CreateInstance<SidePanelCoordinator> 
 ( 
 *browser_ 
 ,  <<<  ...) ...  } ...  
```
### patch
```cpp
      GetUserDataFactory().CreateInstance<BraveSidePanelCoordinator>(*browser_,

```

### match
```cpp
...
>>>
 void 
 BrowserWindowFeatures::TearDownPreBrowserWindowDestruction() 
 {  <<< 
// Tear down embedder features first, in reverse order of initialization.
 ... } ...  
```
### patch
```cpp
void BrowserWindowFeatures_ChromiumImpl::TearDownPreBrowserWindowDestruction() {

```

### match
```cpp
...
>>>
 SidePanelUI 
 * BrowserWindowFeatures::side_panel_ui() 
 {  <<< 
if (webui_browser::IsWebUIBrowserEnabled() && webui_browser_side_panel_ui_) {
    return webui_browser_side_panel_ui_.get();
  }
 ... } ...  
```
### patch
```cpp
SidePanelUI* BrowserWindowFeatures_ChromiumImpl::side_panel_ui() {

```

### match
```cpp
...
>>>
 ToastController 
 * BrowserWindowFeatures::toast_controller() 
 {  <<< 
return toast_service_ ? toast_service_->toast_controller() : nullptr;
 ... } ...  
```
### patch
```cpp
ToastController* BrowserWindowFeatures_ChromiumImpl::toast_controller() {

```

### match
```cpp
...
>>>
 LocationBar 
 * BrowserWindowFeatures::location_bar() 
 {  <<< 
// Return nullptr if not initialized. This can happen in tests where
 ... } ...  
```
### patch
```cpp
LocationBar* BrowserWindowFeatures_ChromiumImpl::location_bar() {

```

### match
```cpp
...
>>>
 const 
 LocationBar 
 * BrowserWindowFeatures::location_bar() const 
 {  <<< 
// Return nullptr if not initialized. This can happen in tests where
 ... } ...  
```
### patch
```cpp
const LocationBar* BrowserWindowFeatures_ChromiumImpl::location_bar() const {

```

### match
```cpp
...
>>>
 FindBarController 
 * BrowserWindowFeatures::GetFindBarController() 
 {  <<< 
if (!find_bar_controller_.get()) {
    CHECK(browser_);
    find_bar_controller_ = std::make_unique<FindBarController>(
        browser_->GetBrowserForMigrationOnly()->window()->CreateFindBar());
    find_bar_controller_->find_bar()->SetFindBarController(
        find_bar_controller_.get());
    find_bar_controller_->ChangeWebContents(
        tab_strip_model_->GetActiveWebContents());
    find_bar_controller_->find_bar()->MoveWindowIfNecessary();
  }
 ... } ...  
```
### patch
```cpp
FindBarController* BrowserWindowFeatures_ChromiumImpl::GetFindBarController() {

```

### match
```cpp
...
>>>
 bool 
 BrowserWindowFeatures::HasFindBarController() const 
 {  <<< 
return find_bar_controller_.get() != nullptr;
 ... } ...  
```
### patch
```cpp
bool BrowserWindowFeatures_ChromiumImpl::HasFindBarController() const {

```

### match
```cpp
...
>>>
 BrowserWindowFeatures::GetUserDataFactoryForTesting() 
 {  <<< 
return GetUserDataFactory();
 ... } ...  
```
### patch
```cpp
BrowserWindowFeatures_ChromiumImpl::GetUserDataFactoryForTesting() {

```

### match
```cpp
...
>>>
 BrowserWindowFeatures::GetUserDataFactory() 
 {  <<< 
static base::NoDestructor<
      ui::UserDataFactoryWithOwner<BrowserWindowInterface>>
      factory;
 ... } ...  
```
### patch
```cpp
BrowserWindowFeatures_ChromiumImpl::GetUserDataFactory() {

```

