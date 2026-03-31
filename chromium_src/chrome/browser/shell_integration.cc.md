### match
```cpp
...
#include "base/i18n/file_util_icu.h"

 #include "base/metrics/histogram.h"
 
 >>> 
#include "base/strings/string_util.h"

 ... 
```
### patch
```cpp
#include "base/notreached.h"

```

### match
```cpp
...
#include "content/public/browser/browser_thread.h"

 #include "content/public/common/content_switches.h"
 
 >>> 
#if BUILDFLAG(IS_CHROMEOS)
#include "ash/constants/ash_switches.h"
#endif
 ... 
```
### patch
```cpp
#include "ui/base/l10n/l10n_util.h"

#if !BUILDFLAG(IS_WIN)
#include "chrome/grit/generated_resources.h"

#define GetAppShortcutsSubdirName GetAppShortcutsSubdirName_UnUsed
#endif

```

### match
```cpp
...
 
 namespace shell_integration { ... 
void DefaultSchemeClientWorker::SetAsDefaultImpl(
    base::OnceClosure on_finished_callback) {
  switch (GetDefaultSchemeClientSetPermission()) {
    case SET_DEFAULT_NOT_ALLOWED:
      // Not allowed, do nothing.
      break;
    case SET_DEFAULT_UNATTENDED:
      SetAsDefaultClientForScheme(scheme_);
      break;
    case SET_DEFAULT_INTERACTIVE:
#if BUILDFLAG(IS_WIN)
      if (interactive_permitted_) {
        win::SetAsDefaultClientForSchemeUsingSystemSettings(
            scheme_, std::move(on_finished_callback));
        // Early return because the function above takes care of calling
        // `on_finished_callback`.
        return;
      }
#endif  // BUILDFLAG(IS_WIN)
      break;
  }
  std::move(on_finished_callback).Run();
}
 } 
 // namespace shell_integration 
 >>> 
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_WIN)
#undef GetAppShortcutsSubdirName
#endif

#if !BUILDFLAG(IS_WIN)
namespace shell_integration {
std::u16string GetAppShortcutsSubdirName() {
  int id = IDS_APP_SHORTCUTS_SUBDIR_NAME_BRAVE_STABLE;
  switch (chrome::GetChannel()) {
    case version_info::Channel::STABLE:
      id = IDS_APP_SHORTCUTS_SUBDIR_NAME_BRAVE_STABLE;
      break;
    case version_info::Channel::BETA:
      id = IDS_APP_SHORTCUTS_SUBDIR_NAME_BRAVE_BETA;
      break;
    case version_info::Channel::DEV:
      id = IDS_APP_SHORTCUTS_SUBDIR_NAME_BRAVE_DEV;
      break;
    case version_info::Channel::CANARY:
      id = IDS_APP_SHORTCUTS_SUBDIR_NAME_BRAVE_NIGHTLY;
      break;
    case version_info::Channel::UNKNOWN:
      id = IDS_APP_SHORTCUTS_SUBDIR_NAME_BRAVE_DEVELOPMENT;
      break;
    default:
      NOTREACHED() << "All possible channels are handled above.";
  }

  return l10n_util::GetStringUTF16(id);
}
}  // namespace shell_integration
#endif  // !BUILDFLAG(IS_WIN)

```

