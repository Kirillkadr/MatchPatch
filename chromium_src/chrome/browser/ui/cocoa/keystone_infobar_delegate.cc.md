### match
```cpp
...
#include "base/functional/bind.h"

 #include "base/task/single_thread_task_runner.h"
 
 >>> 
#include "chrome/browser/infobars/confirm_infobar_creator.h"

 ... 
```
### patch
```cpp
#include "brave/browser/updater/buildflags.h"

```

### match
```cpp
...
#include "content/public/browser/web_contents.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
namespace {

void ShowUpdaterPromotionInfoBarOnUISequence() {
  // If the user clicked the "don't ask again" button at some point in the
  // past, or if the "don't ask about the default browser" command-line switch
  // is present, bail out.  That command-line switch is recycled here because
  // it's likely that the set of users that don't want to be nagged about the
  // default browser also don't want to be nagged about the update check.
  // (Automated testers, I'm thinking of you...)
  BrowserWindowInterface* browser =
      GlobalBrowserCollection::GetInstance()->GetLastActiveBrowser();
  if (!browser || !browser->GetProfile() ||
      !browser->GetProfile()->GetPrefs()->GetBoolean(
          prefs::kShowUpdatePromotionInfoBar) ||
      base::CommandLine::ForCurrentProcess()->HasSwitch(
          switches::kNoDefaultBrowserCheck)) {
    return;
  }
  KeystonePromotionInfoBarDelegate::Create(
      browser->GetTabStripModel()->GetActiveWebContents());
}

}
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_OMAHA4)
#include "brave/browser/updater/features.h"
#define ShowUpdaterPromotionInfoBar ShowUpdaterPromotionInfoBar_ChromiumImpl
#endif


```

### match
```cpp
...
 
 void ShowUpdaterPromotionInfoBar() { ... 
content::GetUIThreadTaskRunner({})->PostTask(
      FROM_HERE, base::BindOnce(&ShowUpdaterPromotionInfoBarOnUISequence));
 } 
 >>> 
 ... 
```
### patch
```cpp

#if BUILDFLAG(ENABLE_OMAHA4)
#undef ShowUpdaterPromotionInfoBar
void ShowUpdaterPromotionInfoBar() {
  if (brave_updater::ShouldUseOmaha4()) {
    ShowUpdaterPromotionInfoBar_ChromiumImpl();
  }
}
#endif
```

