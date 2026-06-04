### match
```cpp
...
#include <tuple>

 #include <utility>
 
 >>> 
#include "base/check_op.h"

 ...
```
### patch
```cpp
#include <string>
#include "components/grit/brave_components_strings.h"
#include "ui/base/l10n/l10n_util.h"
#include "ui/strings/grit/ui_strings.h"

```

### match
```cpp
...
 
 >>> 
Accelerator::Accelerator(const KeyEvent& key_event)
    : key_code_(key_event.key_code()) ...
```
### patch
```cpp
namespace {
// We make significant changes to the `ApplyLongFormModifiers` method, and
// instead of adding multiple patches it's easier to implement our own version.
std::vector<std::u16string> BraveGetLongFormModifiers(bool shift,
                                                      bool ctrl,
                                                      bool alt,
                                                      bool cmd,
                                                      bool fn) {
  std::vector<std::u16string> modifiers;
  if (cmd) {
#if BUILDFLAG(IS_MAC)
    modifiers.push_back(l10n_util::GetStringUTF16(IDS_APP_COMMAND_KEY));
#elif BUILDFLAG(IS_WIN)
    modifiers.push_back(l10n_util::GetStringUTF16(IDS_APP_WINDOWS_KEY));
#else
    modifiers.push_back(l10n_util::GetStringUTF16(IDS_APP_META_KEY));
#endif
  }

  if (ctrl) {
    modifiers.push_back(l10n_util::GetStringUTF16(IDS_APP_CTRL_KEY));
  }

  if (shift) {
    modifiers.push_back(l10n_util::GetStringUTF16(IDS_APP_SHIFT_KEY));
  }

  if (alt) {
    modifiers.push_back(l10n_util::GetStringUTF16(IDS_APP_ALT_KEY));
  }

  return modifiers;
}
}  // namespace

```

### match
```cpp
...
 >>> 
std::vector<std::u16string> shortcut_vector;
 ...
```
### patch
```cpp
    return BraveGetLongFormModifiers(IsShiftDown(), IsCtrlDown(), IsAltDown(),
                                   IsCmdDown(), IsFunctionDown());

```

