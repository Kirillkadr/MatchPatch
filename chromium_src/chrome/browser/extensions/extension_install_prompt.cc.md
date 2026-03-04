### match
```
...
#include "base/task/single_thread_task_runner.h"

 #include "base/values.h"
 
 >>> 
#include "chrome/browser/extensions/extension_install_prompt_show_params.h"

 ... 
```
### patch
```
#include "brave/grit/brave_generated_resources.h"

```

### match
```
...
>>>
 std::u16string 
 ExtensionInstallPrompt::Prompt::GetDialogTitle() const 
 {  <<< 
int id = -1;
 ... } ...  
```
### patch
```
std::u16string ExtensionInstallPrompt::Prompt::GetDialogTitle_ChromiumImpl() const {

```

### match
```
...
 
 bool ExtensionInstallPrompt::AutoConfirmPromptIfEnabled() { ... 
NOTREACHED();
 } 
 >>> 
 ... 
```
### patch
```

std::u16string ExtensionInstallPrompt::Prompt::GetDialogTitle() const {
  if (type_ == ExtensionInstallPrompt::INSTALL_PROMPT) {
    return l10n_util::GetStringUTF16(
        IDS_UNVETTED_EXTENSION_INSTALL_PROMPT_TITLE);
  }
  return GetDialogTitle_ChromiumImpl();
}
```

