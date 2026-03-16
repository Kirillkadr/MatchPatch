### match
```
...
// found in the LICENSE file.
 #include "chrome/browser/download/download_file_picker.h"
 
 >>> 
#include "base/files/file_path.h"

 ... 
```
### patch
```
#include <string>

#include "base/check.h"

```

### match
```
...
#include "chrome/browser/ui/chrome_select_file_policy.h"

 #include "components/download/public/common/base_file.h"
 
 >>> 
#include "content/public/browser/browser_context.h"

 ... 
```
### patch
```
#include "components/download/public/common/download_item.h"

```

### match
```
...
#include "content/public/browser/download_manager.h"

 #include "content/public/browser/web_contents.h"
 
 >>> 
#include "ui/shell_dialogs/selected_file_info.h"

 ... 
```
### patch
```
#include "third_party/blink/public/mojom/choosers/file_chooser.mojom.h"
#include "ui/shell_dialogs/select_file_dialog.h"
#include "url/origin.h"

```

### match
```
...
#include "url/origin.h"

 #include "ui/shell_dialogs/selected_file_info.h"
 
 >>> 
#if BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_WIN)
#include "chrome/browser/ui/browser_window.h"
#include "chrome/browser/ui/browser_window/public/browser_window_interface_iterator.h"
#include "ui/aura/window.h"
#endif
 ... 
```
### patch
```
#if !BUILDFLAG(IS_ANDROID)
#include "brave/browser/ui/brave_file_select_utils.h"
#endif


```

### match
```
...
#include "ui/aura/window.h"

 #endif 
 >>> 
 ... 
```
### patch
```
namespace {

std::u16string GetTitle(content::RenderFrameHost* render_frame_host,
                        const std::u16string& original_title,
                        const GURL* caller) {
#if BUILDFLAG(IS_ANDROID)
  return original_title;
#else
  if (!render_frame_host) {
    return original_title;
  }
  CHECK(caller);
  return brave::GetFileSelectTitle(
      content::WebContents::FromRenderFrameHost(render_frame_host),
      render_frame_host->GetLastCommittedOrigin(), url::Origin::Create(*caller),
      brave::FileSelectTitleType::kSave);
#endif
}

}  // namespace


```

### match
```
...
 
 DownloadFilePicker::DownloadFilePicker(download::DownloadItem* item,
                                       const base::FilePath& suggested_path,
                                       ConfirmationCallback callback)
    : suggested_path_(suggested_path),
      file_selected_callback_(std::move(callback)),
      download_item_(item) { ... 
if (!caller.is_valid() && render_frame_host &&
      render_frame_host->GetLastCommittedURL().SchemeIsBlob()) {
    caller = render_frame_host->GetLastCommittedOrigin().GetURL();
  }  >>> 
 select_file_dialog_->SelectFile(
      ui::SelectFileDialog::SELECT_SAVEAS_FILE, std::u16string(),
      suggested_path_, &file_type_info, 0, base::FilePath::StringType(),
      owning_window, &caller);  <<<  ...} ...  
```
### patch
```
  select_file_dialog_- SelectFile(type, GetTitle(render_frame_host, title, caller), default_path,
             file_types, file_type_index, default_extension, owning_window,
             caller);

```

