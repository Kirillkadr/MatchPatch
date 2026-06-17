### match
```cpp
...
// found in the LICENSE file.
 #include "components/translate/core/browser/translate_script.h"
 
 >>> 
 ...
```
### patch
```cpp
#include "base/functional/callback.h"
#include "base/strings/strcat.h"
#include "base/strings/to_string.h"
#include "base/task/sequenced_task_runner.h"
#include "brave/components/constants/brave_services_key.h"
#include "brave/components/translate/core/common/brave_translate_constants.h"
#include "brave/components/translate/core/common/brave_translate_features.h"
#include "components/grit/brave_components_resources.h"
#include "third_party/abseil-cpp/absl/strings/str_format.h"
#include "ui/base/resource/resource_bundle.h"

```

### match
```cpp
...
 namespace 
 translate 
 { 
 >>> 
 ... } ...
```
### patch
```cpp
namespace google_apis {
std::string GetAPIKey() {
  return BUILDFLAG(BRAVE_SERVICES_KEY);
}
}  // namespace google_apis

```

### match
```cpp
...
const char TranslateScript::kScriptURL[] =
    "https://translate.googleapis.com/translate_a/element.js";
>>> ...
```
### patch
```cpp
#define TranslateScript ChromiumTranslateScript

```

### match
```cpp
...
 
 namespace translate { ... 
 >>> 
 } ...  
```
### patch
```cpp
#undef TranslateScript
// Redirect the translate script request to the Brave endpoints.
GURL ChromiumTranslateScript::AddHostLocaleToUrl(const GURL& url) {
  GURL result = ::translate::AddHostLocaleToUrl(url);
  const GURL google_translate_script(kScriptURL);
  if (result.host() == google_translate_script.host()) {
    const GURL brave_translate_script(kBraveTranslateScriptURL);
    GURL::Replacements replaces;
    replaces.SetHostStr(brave_translate_script.host());
    replaces.SetPathStr(brave_translate_script.path());
    return result.ReplaceComponents(replaces);
  }
  return result;
}

void TranslateScript::Request(RequestCallback callback, bool is_incognito) {
  if (!IsBraveTranslateGoAvailable()) {
    base::SequencedTaskRunner::GetCurrentDefault()->PostTask(
        FROM_HERE, base::BindOnce(std::move(callback), false));
    return;
  }
  ChromiumTranslateScript::Request(std::move(callback), is_incognito);
}

void TranslateScript::OnScriptFetchComplete(bool success,
                                            const std::string& data) {
  const std::string new_data = base::StrCat(
      {absl::StrFormat("const useGoogleTranslateEndpoint = %s;",
                       base::ToString(translate::UseGoogleTranslateEndpoint())),
       absl::StrFormat("const braveTranslateStaticPath = '%s';",
                       kBraveTranslateStaticPath),
       ui::ResourceBundle::GetSharedInstance().LoadDataResourceString(
           IDR_BRAVE_TRANSLATE_JS),
       data});
  ChromiumTranslateScript::OnScriptFetchComplete(success, new_data);
}


```

