### match
```cpp
...
#include "chrome/browser/ui/startup/infobar_utils.h"

 #include "base/command_line.h"
 
 >>> 
#include "base/metrics/histogram_functions.h"

 ... 
```
### patch
```cpp
#include "base/check.h"

```

### match
```cpp
...
#include "base/metrics/histogram_functions.h"

 #include "base/rand_util.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ... 
```
### patch
```cpp
#include "brave/browser/infobars/dev_channel_deprecation_infobar_delegate.h"
#include "brave/browser/ui/startup/brave_obsolete_system_infobar_delegate.h"

```

### match
```cpp
...
#include "chrome/browser/ui/startup/startup_launch_infobar_manager_impl.h"  // nogncheck

 #endif 
 >>> 
 ... 
```
### patch
```cpp
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC)
#define ObsoleteSystemInfoBarDelegate BraveObsoleteSystemInfoBarDelegate
#endif


```

### match
```cpp
...
>>>
 void 
 AddInfoBarsIfNecessary 
 ( 
 BrowserWindowInterface* browser 
 ,  <<< 
Profile* profile
 ... ) ...  
```
### patch
```cpp
class BraveGoogleKeysInfoBarDelegate {
 public:
  static void Create(infobars::ContentInfoBarManager* infobar_manager) {
    // lulz
  }
};

void AddInfoBarsIfNecessary_ChromiumImpl(BrowserWindowInterface* browser,

```

### match
```cpp
...
 
 void AddInfoBarsIfNecessary_ChromiumImpl(BrowserWindowInterface* browser,
Profile* profile,
                            const base::CommandLine& startup_command_line,
                            chrome::startup::IsFirstRun is_first_run,
                            bool is_web_app,
                            bool is_post_crash_launch,
                            bool was_restarted) { ... 
 
 if (should_display_bubble) { ...   >>> 
 SessionCrashedBubble::ShowIfNotOffTheRecordProfile 
 (  <<<  ...) ...  } ...  } ...  
```
### patch
```cpp
    SessionCrashedBubble::ShowIfNotOffTheRecordProfileBrave(

```

### match
```cpp
...
 
 void AddInfoBarsIfNecessary_ChromiumImpl(BrowserWindowInterface* browser,
Profile* profile,
                            const base::CommandLine& startup_command_line,
                            chrome::startup::IsFirstRun is_first_run,
                            bool is_web_app,
                            bool is_post_crash_launch,
                            bool was_restarted) { ... 
 
 if (!google_apis::HasAPIKeyConfigured()) { ...   >>> 
 GoogleApiKeysInfoBarDelegate::Create(infobar_manager);  <<<  ...} ...  } ...  
```
### patch
```cpp
    BraveGoogleKeysInfoBarDelegate::Create(infobar_manager);

```

### match
```cpp
...
 
 void AddInfoBarsIfNecessary_ChromiumImpl(BrowserWindowInterface* browser,
Profile* profile,
                            const base::CommandLine& startup_command_line,
                            chrome::startup::IsFirstRun is_first_run,
                            bool is_web_app,
                            bool is_post_crash_launch,
                            bool was_restarted) { ... 
// !BUILDFLAG(IS_CHROMEOS) && !BUILDFLAG(IS_ANDROID)
 } 
 >>> 
 ... 
```
### patch
```cpp

#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC)
#undef ObsoleteSystemInfoBarDelegate
#endif

void AddInfoBarsIfNecessary(BrowserWindowInterface* browser,
                            Profile* profile,
                            const base::CommandLine& startup_command_line,
                            chrome::startup::IsFirstRun is_first_run,
                            bool is_web_app,
                            bool is_post_crash_launch,
                            bool was_restarted) {
  AddInfoBarsIfNecessary_ChromiumImpl(browser, profile, startup_command_line,
                                      is_first_run, is_web_app,
                                      is_post_crash_launch, was_restarted);

  TabStripModel* tab_strip_model = browser->GetTabStripModel();
  if (!browser || !profile || tab_strip_model->count() == 0) {
    return;
  }

  if (IsKioskModeEnabled()) {
    return;
  }

  if (!startup_command_line.HasSwitch(switches::kTestType) &&
      !IsAutomationEnabled()) {
    static bool infobars_shown = false;
    if (infobars_shown) {
      return;
    }
    infobars_shown = true;

    content::WebContents* web_contents =
        tab_strip_model->GetActiveWebContents();
    DCHECK(web_contents);
    infobars::ContentInfoBarManager* infobar_manager =
        infobars::ContentInfoBarManager::FromWebContents(web_contents);
    DevChannelDeprecationInfoBarDelegate::CreateIfNeeded(infobar_manager);
  }
}
```

