### match
```
...
// found in the LICENSE file.
 #include "chrome/browser/download/bubble/download_display_controller.h"
 
 >>> 
#include "base/functional/bind.h"

 ... 
```
### patch
```
#include "base/check.h"

```

### match
```
...
#include "chrome/browser/ui/views/frame/browser_view.h"

 #include "chrome/browser/ui/views/frame/immersive_mode_controller.h"
 
 >>> 
#include "components/download/public/common/download_danger_type.h"

 ... 
```
### patch
```
#include "chrome/browser/ui/web_applications/app_browser_controller.h"

```

### match
```
...
#include "chrome/browser/ui/fullscreen_util_mac.h"

 #endif 
 >>> 
 ... 
```
### patch
```
#define DownloadDisplayController DownloadDisplayControllerChromium


```

### match
```
...
 
 void DownloadDisplayController::MaybeShowButtonWhenCreated() { ... 
if (display_->IsShowing()) {
    base::Time disappearance_time =
        info.last_completed_time + kToolbarIconVisibilityTimeInterval;
    base::TimeDelta interval_until_disappearance =
        disappearance_time - base::Time::Now();
    // Avoid passing a negative time interval.
    ScheduleToolbarDisappearance(
        std::max(base::TimeDelta(), interval_until_disappearance));
  }
 } 
 >>> 
 ... 
```
### patch
```
#undef DownloadDisplayController

void DownloadDisplayController::UpdateToolbarButtonState(
    const DownloadBubbleDisplayInfo& info,
    const DownloadDisplay::ProgressInfo& progress_info) {
  DownloadDisplayControllerChromium::UpdateToolbarButtonState(info,
                                                              progress_info);

  if (info.all_models_size == 0) {
    return;
  }

  if (display_->IsShowing()) {
    return;
  }

  // Show toolbar if there's at least one in-progress download item.
  // Upstream doesn't show toolbar button when only dangerous files are
  // in-progress. We cannot use DownloadBubbleDisplayInfo's in_progress_count
  // here because it doesn't include dangerous files.
  std::vector<DownloadUIModel::DownloadUIModelPtr> all_models;
  bubble_controller_->update_service()->GetAllModelsToDisplay(
      all_models, GetWebAppIdForBrowser(browser_),
      /*force_backfill_download_items=*/true);
  DCHECK(!all_models.empty());
  for (const auto& model : all_models) {
    if (model->GetState() == download::DownloadItem::IN_PROGRESS) {
      ShowToolbarButton();
      return;
    }
  }
}
```

