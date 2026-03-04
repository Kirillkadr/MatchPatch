### match
```
...
#include "components/browser_ui/util/android/url_constants.h"

 #include "components/omnibox/browser/autocomplete_classifier.h"
 
 >>> 
#include "components/omnibox/browser/autocomplete_controller_config.h"

 ... 
```
### patch
```
#include "components/omnibox/browser/autocomplete_controller.h"

```

### match
```
...
#include "url/android/gurl_android.h"

 #include "url/gurl.h"
 
 >>> 
// Must come after all headers that specialize FromJniType() / ToJniType().
 ... 
```
### patch
```
#include "brave/browser/autocomplete/brave_autocomplete_scheme_classifier.h"

```

### match
```
...
 void AutocompleteControllerAndroid::Start(
    JNIEnv* env,
    const JavaRef<jstring>& j_text,
    int32_t j_cursor_pos,
    const JavaRef<jstring>& j_desired_tld,
    const JavaRef<jstring>& j_current_url,
    ::metrics::OmniboxEventProto::PageClassification page_classification,
    ::omnibox::ToolMode tool_mode,
    bool prevent_inline_autocomplete,
    bool prefer_keyword,
    bool allow_exact_keyword_match,
    bool want_asynchronous_matches) { ... 
 AutocompleteInput ( ...   >>> 
 ChromeAutocompleteSchemeClassifier(profile_) 
 ) 
 ;  <<< ... } ...  
```
### patch
```
                             BraveAutocompleteSchemeClassifier(profile_));

```

### match
```
...
 void AutocompleteControllerAndroid::StartPrefetch(
    JNIEnv* env,
    const JavaRef<jstring>& j_current_url,
    ::metrics::OmniboxEventProto::PageClassification page_classification,
    const JavaRef<jobject>& j_web_contents) { ...   >>> 
 ChromeAutocompleteSchemeClassifier(profile_) 
 ) 
 ;  <<< ... } ...  
```
### patch
```
                          BraveAutocompleteSchemeClassifier(profile_));

```

### match
```
...
 void AutocompleteControllerAndroid::OnOmniboxFocused(
    JNIEnv* env,
    const JavaRef<jstring>& j_omnibox_text,
    const JavaRef<jstring>& j_current_url,
    ::metrics::OmniboxEventProto::PageClassification page_classification,
    ::omnibox::ToolMode tool_mode,
    const JavaRef<jstring>& j_current_title) { ... 
 AutocompleteInput ( ...   >>> 
 ChromeAutocompleteSchemeClassifier(profile_) 
 ) 
 ;  <<< ... } ...  
```
### patch
```
                             BraveAutocompleteSchemeClassifier(profile_));

```

