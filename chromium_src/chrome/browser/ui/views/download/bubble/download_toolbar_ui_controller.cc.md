### match
```cpp
...
 #include "chrome/browser/download/bubble/download_bubble_ui_controller.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "chrome/browser/download/bubble/download_bubble_update_service.h"
#include "chrome/browser/download/bubble/download_bubble_update_service_factory.h"

```

### match
```cpp
...
 #include "chrome/browser/download/bubble/download_display_controller.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "chrome/browser/download/download_ui_model.h"

```

### match
```cpp
...
 #include "components/safe_browsing/core/common/safe_browsing_prefs.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "components/vector_icons/vector_icons.h"

```

### match
```cpp
...
 #include "ui/base/metadata/metadata_impl_macros.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "ui/base/models/image_model.h"

```

### match
```cpp
...
 
 namespace { ... 
// it.
 constexpr base::TimeDelta kAutoClosePartialViewDelay = base::Seconds(5); 
 >>> 
 ... } ...
```
### patch
```cpp
SkColor GetIconColor(SkColor chromium_color,
                     DownloadDisplay::IconState state,
                     DownloadDisplay::IconActive active,
                     const ui::ColorProvider* color_provider) {
  // Apply active color only when download is completed and user doesn't
  // interact with this button.
  if (state == DownloadDisplay::IconState::kComplete &&
      active == DownloadDisplay::IconActive::kActive) {
    return color_provider->GetColor(kColorDownloadToolbarButtonActive);
  }

  // Otherwise, always use inactive color.
  return color_provider->GetColor(kColorDownloadToolbarButtonInactive);
}

```

### match
```cpp
...
>>>
 DownloadToolbarUIController 
 * 
 DownloadToolbarUIController::From 
 ( 
<<< 
...) ...
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl* DownloadToolbarUIController_ChromiumImpl::From(

```

### match
```cpp
...
>>>
 DownloadToolbarUIController::DownloadToolbarUIController 
 ( 
<<< 
...) ...
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl::DownloadToolbarUIController_ChromiumImpl(

```

### match
```cpp
...
 DownloadToolbarUIController_ChromiumImpl::DownloadToolbarUIController_ChromiumImpl ... 
 
 base::BindRepeating ( ... 
>>> 
 &DownloadToolbarUIController::AutoClosePartialView 
 , 
<<< 
...) ...
```
### patch
```cpp
&DownloadToolbarUIController_ChromiumImpl::AutoClosePartialView,

```

### match
```cpp
...
>>>
 DownloadToolbarUIController::~DownloadToolbarUIController() 
 { 
<<< 
...} ...  
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl::~DownloadToolbarUIController_ChromiumImpl() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::Init() 
 { 
<<< 
// `controller_` can call `Show()` synchronously so it must be initialized
 ... } ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::Init() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::TearDownPreBrowserWindowDestruction() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::TearDownPreBrowserWindowDestruction() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::Show() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::Show() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::Hide() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::Hide() {

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::IsShowing() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::IsShowing() const {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::Enable() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::Enable() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::Disable() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::Disable() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::UpdateDownloadIcon 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::UpdateDownloadIcon(

```

### match
```cpp
...
 
 if (auto* container = GetPinnedToolbarActions(browser_view_)) { ... 
 container->PostOrQueueActionAfterAnimation ( ... 
 
 base::BindOnce ( ... 
>>> 
 &DownloadToolbarUIController::ShowPendingDownloadStartedAnimation 
 , 
<<< 
...) ...  ) ...  } ...  
```
### patch
```cpp
          &DownloadToolbarUIController_ChromiumImpl::ShowPendingDownloadStartedAnimation,

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::AnnounceAccessibleAlertNow 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::AnnounceAccessibleAlertNow(

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::IsFullscreenWithParentViewHidden() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::IsFullscreenWithParentViewHidden() const {

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::ShouldShowExclusiveAccessBubble() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::ShouldShowExclusiveAccessBubble() const {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OpenSecuritySubpage 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OpenSecuritySubpage(

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::ShowDetails() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::ShowDetails() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::HideDetails() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::HideDetails() {

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::IsShowingDetails() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::IsShowingDetails() const {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::UpdateIcon() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::UpdateIcon() {

```

### match
```cpp
...
 
 void DownloadToolbarUIController_ChromiumImpl::UpdateIcon() { ... 
>>> 
 action_item_->SetImage(ui::ImageModel::FromVectorIcon(*new_icon, icon_color)); 
<<< 
// Update the toolbar button's tooltip.
 ... } ...  
```
### patch
```cpp
  action_item_->SetImage(ui::ImageModel::FromVectorIcon(*new_icon, GetIconColor(icon_color, state_, active_,
                                    browser_view_->GetColorProvider()));

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OpenPrimaryDialog() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OpenPrimaryDialog() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OpenSecurityDialog 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OpenSecurityDialog(

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::CloseDialog 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::CloseDialog(

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OnSecurityDialogButtonPress 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OnSecurityDialogButtonPress(

```

### match
```cpp
...
 
 if (model.GetDangerType() ==
          download::DOWNLOAD_DANGER_TYPE_UNCOMMON_CONTENT &&
      command == DownloadCommands::DISCARD) { ... 
>>> 
 FROM_HERE 
 , 
 base::BindOnce 
 ( 
 &DownloadToolbarUIController::ShowIphPromo 
 , 
<<< 
...) ...  } ...  
```
### patch
```cpp
        FROM_HERE, base::BindOnce(&DownloadToolbarUIController_ChromiumImpl::ShowIphPromo,

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OnDialogInteracted() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OnDialogInteracted() {

```

### match
```cpp
...
>>>
 DownloadToolbarUIController::PreventDialogCloseOnDeactivate() 
 { 
<<< 
...} ...  
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl::PreventDialogCloseOnDeactivate() {

```

### match
```cpp
...
>>>
 DownloadToolbarUIController::GetWeakPtr() 
 { 
<<< 
...} ...  
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl::GetWeakPtr() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OnBrowserActivated 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OnBrowserActivated(

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OnBrowserDeactivated 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OnBrowserDeactivated(

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::DeactivateAutoClose() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::DeactivateAutoClose() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::InvokeUI() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::InvokeUI() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::ShowPendingDownloadStartedAnimation() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::ShowPendingDownloadStartedAnimation() {

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::IsProgressRingInDownloadingStateForTesting() 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::IsProgressRingInDownloadingStateForTesting() {

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::IsProgressRingInDormantStateForTesting() 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::IsProgressRingInDormantStateForTesting() {

```

### match
```cpp
...
>>>
 views::ImageView 
 * DownloadToolbarUIController::GetImageBadgeForTesting() 
 { 
<<< 
...} ...  
```
### patch
```cpp
views::ImageView* DownloadToolbarUIController_ChromiumImpl::GetImageBadgeForTesting() {

```

### match
```cpp
...
>>>
 DownloadToolbarUIController::BubbleCloser::BubbleCloser 
 ( 
<<< 
...) ...  
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl::BubbleCloser::BubbleCloser(

```

### match
```cpp
...
>>>
 DownloadToolbarUIController::BubbleCloser::~BubbleCloser() = default; 
<<< 
...
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl::BubbleCloser::~BubbleCloser() = default;

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::BubbleCloser::OnEvent 
 ( 
<<< 
...) ...  
```
### patch
```cpp

void DownloadToolbarUIController_ChromiumImpl::BubbleCloser::OnEvent(

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::BubbleCloser::OnWidgetDestroyed 
 ( 
<<< 
...) ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::BubbleCloser::OnWidgetDestroyed(

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::CreateBubbleDialogDelegate() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::CreateBubbleDialogDelegate() {

```

### match
```cpp
...
 
 bubble_delegate->RegisterWindowClosingCallback ( ... 
>>> 
 base::BindOnce 
 ( 
 &DownloadToolbarUIController::OnBubbleClosing 
 , 
<<< 
...) ...  ) ...  
```
### patch
```cpp
      base::BindOnce(&DownloadToolbarUIController_ChromiumImpl::OnBubbleClosing,

```

### match
```cpp
...
 
 if (is_primary_partial_view_) { ... 
 
 bubble_delegate_->SetCloseCallback ( ... 
>>> 
 base::BindOnce 
 ( 
 &DownloadToolbarUIController::OnPartialViewClosed 
 , 
<<< 
...) ...  ) ...  } ...  
```
### patch
```cpp
        base::BindOnce(&DownloadToolbarUIController_ChromiumImpl::OnPartialViewClosed,

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OnBubbleClosing() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OnBubbleClosing() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OnPartialViewClosed() 
 { 
<<< 
// We use PostTask to avoid calling the FocusAndActivateWindow
 ... } ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OnPartialViewClosed() {

```

### match
```cpp
...
>>>
 FROM_HERE 
 , 
 base::BindOnce 
 ( 
 &DownloadToolbarUIController::ShowIphPromo 
 , 
<<< 
...) ...  
```
### patch
```cpp
      FROM_HERE, base::BindOnce(&DownloadToolbarUIController_ChromiumImpl::ShowIphPromo,

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::ShowIphPromo() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::ShowIphPromo() {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::AutoClosePartialView() 
 { 
<<< 
// Nothing to do if the bubble is not open.
 ... } ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::AutoClosePartialView() {

```

### match
```cpp
...
>>>
 DownloadToolbarUIController::GetPrimaryViewModels() 
 { 
<<< 
...} ...  
```
### patch
```cpp
DownloadToolbarUIController_ChromiumImpl::GetPrimaryViewModels() {

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::ShouldShowBubbleAsInactive() const 
 { 
<<< 
// The bubble can either be shown as active or inactive. When the current
 ... } ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::ShouldShowBubbleAsInactive() const {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::CloseAutofillPopup() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::CloseAutofillPopup() {

```

### match
```cpp
...
>>>
 bool 
 DownloadToolbarUIController::ShouldShowScanningAnimation() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
bool DownloadToolbarUIController_ChromiumImpl::ShouldShowScanningAnimation() const {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::UpdateIconDormant() 
 { 
<<< 
// Ensure no updates are attempted once BrowserView destruction has started or
 ... } ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::UpdateIconDormant() {

```

### match
```cpp
...
>>>
 DownloadDisplay::IconState 
 DownloadToolbarUIController::GetIconState() const 
 { 
<<< 
...} ...  
```
### patch
```cpp
DownloadDisplay::IconState DownloadToolbarUIController_ChromiumImpl::GetIconState() const {

```

### match
```cpp
...
>>>
 void 
 DownloadToolbarUIController::OnAnyRowRemoved() 
 { 
<<< 
...} ...  
```
### patch
```cpp
void DownloadToolbarUIController_ChromiumImpl::OnAnyRowRemoved() {

```

### match
```cpp
...
 
 void DownloadToolbarUIController_ChromiumImpl::OnAnyRowRemoved() { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp

void DownloadToolbarUIController::UpdateIcon() {
  DownloadToolbarUIController_ChromiumImpl::UpdateIcon();

  if (!action_item_.get()) {
    return;
  }

  auto* button = GetDownloadsButton(browser_view_);
  if (!button) {
    return;
  }

  // Use an exclamation point icon while there's an insecure download in the
  // download models.
  if (HasInsecureDownloads()) {
    auto icon_color = browser_view_->GetColorProvider()->GetColor(
        ui::kColorAlertMediumSeverityIcon);
    button->SetIconEnabledColorsOverride(icon_color);
    button->SetVectorIcon(vector_icons::kNotSecureWarningIcon);
    const gfx::VectorIcon* new_icon = &vector_icons::kNotSecureWarningIcon;
    const int icon_size = action_item_->GetImage().Size().height();
    action_item_->SetImage(
        ui::ImageModel::FromVectorIcon(*new_icon, icon_color, icon_size));
  } else {
    button->SetIconEnabledColorsOverride(std::nullopt);
  }
}

bool DownloadToolbarUIController::HasInsecureDownloads() {
  auto* update_service = DownloadBubbleUpdateServiceFactory::GetForProfile(
      browser_view_->GetProfile());
  if (!update_service || !update_service->IsInitialized()) {
    return false;
  }

  std::vector<DownloadUIModel::DownloadUIModelPtr> all_models;
  update_service->GetAllModelsToDisplay(all_models, /*web_app_id=*/nullptr,
                                        /*force_backfill_download_items=*/true);

  return std::ranges::any_of(all_models, [](const auto& model) {
    return (model->GetInsecureDownloadStatus() ==
                download::DownloadItem::InsecureDownloadStatus::BLOCK ||
            model->GetInsecureDownloadStatus() ==
                download::DownloadItem::InsecureDownloadStatus::WARN);
  });
}
```

