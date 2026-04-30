### match
```cpp
...
#include <string_view>

 #include <utility>
 
 >>> 
#include "base/auto_reset.h"

 ... 
```
### patch
```cpp
#include <optional>


```

### match
```cpp
...
#include "base/format_macros.h"

 #include "base/functional/bind.h"
 
 >>> 
#include "base/metrics/histogram_functions.h"

 ... 
```
### patch
```cpp
#include "base/memory/raw_ptr.h"

```

### match
```cpp
...
#include "base/trace_event/trace_event.h"

 #include "base/trace_event/typed_macros.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ... 
```
### patch
```cpp
#include "brave/components/commander/common/buildflags/buildflags.h"
#include "brave/components/omnibox/browser/brave_search_provider.h"

```

### match
```cpp
...
#include "components/search_engines/util.h"

 #include "components/strings/grit/components_strings.h"
 
 >>> 
#include "content/public/browser/navigation_handle.h"

 ... 
```
### patch
```cpp
#include "components/vector_icons/vector_icons.h"

```

### match
```cpp
...
>>>
 #if 
 BUILDFLAG(GOOGLE_CHROME_BRANDING) 
 
 
 #include "components/vector_icons/vector_icons.h"  // nogncheck
  <<<  ...
```
### patch
```cpp
#if BUILDFLAG(ENABLE_COMMANDER)
#include "brave/components/commander/common/constants.h"
#include "brave/components/commander/common/features.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 void EmitAcceptedKeywordSuggestionHistogram(
    OmniboxEventProto::KeywordModeEntryMethod entry_method,
    const TemplateURL* turl) { ... 
if (turl != nullptr) {
    base::UmaHistogramEnumeration(
        kKeywordModeUsageByEngineTypeAcceptedHistogramName,
        turl->GetBuiltinEngineType(),
        BuiltinEngineType::KEYWORD_MODE_ENGINE_TYPE_MAX);
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
[[nodiscard]] std::optional<base::AutoReset<bool>>
SetInputIsPastedFromClipboard(OmniboxController* omnibox_controller,
                              bool is_input_pasted) {
  CHECK(omnibox_controller);

  if (auto* autocomplete_controller =
          omnibox_controller->autocomplete_controller()) {
    if (auto* search_provider = autocomplete_controller->search_provider()) {
      return search_provider->AsBraveSearchProvider()
          ->SetInputIsPastedFromClipboard(is_input_pasted);
    }
  }
  return std::nullopt;
}

```

### match
```cpp
...
>>>
 ui::ImageModel 
 OmniboxEditModel::GetSuperGIcon 
 ( 
 int image_size 
 ,  <<< 
bool dark_mode
 ... ) ...  
```
### patch
```cpp
ui::ImageModel OmniboxEditModel::GetSuperGIcon_Unused(int image_size,

```

### match
```cpp
...
>>>
 bool 
 OmniboxEditModel::CanPasteAndGo(const std::u16string& text) const 
 {  <<< 
if (!controller_->client()->IsPasteAndGoEnabled()) {
    return false;
  }
 ... } ...  
```
### patch
```cpp
bool OmniboxEditModel::CanPasteAndGo_Chromium(const std::u16string& text) const {

```

### match
```cpp
...
>>>
 void 
 OmniboxEditModel::PasteAndGo 
 ( 
 const std::u16string& text 
 ,  <<< 
base::TimeTicks match_selection_timestamp
 ... ) ...  
```
### patch
```cpp
void OmniboxEditModel::PasteAndGo_Chromium(const std::u16string& text,

```

### match
```cpp
...
 
 void OmniboxEditModel::PasteAndGo_Chromium(const std::u16string& text,
base::TimeTicks match_selection_timestamp) { ...   >>> 
 DCHECK(CanPasteAndGo(text));  <<< 
if (view_) {
    view_->RevertAll();
  }
 ... } ...  
```
### patch
```cpp
  DCHECK(CanPasteAndGo_Chromium(text));

```

### match
```cpp
...
 
 void OmniboxEditModel::StartZeroSuggestRequest(
    bool user_clobbered_permanent_text) { ... 
 
 if (std::optional<lens::proto::LensOverlaySuggestInputs> suggest_inputs =
          controller_->client()->GetLensOverlaySuggestInputs()) { ... 
input_.set_lens_overlay_suggest_inputs(*suggest_inputs);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
   auto pasted = SetInputIsPastedFromClipboard(
      controller_, paste_state_ != PasteState::kNone);

```

### match
```cpp
...
 
 void OmniboxEditModel::RecordAiModeMetrics(const std::u16string& query_text,
                                           bool activated,
                                           bool via_keyboard) { ... 
base::UmaHistogramBoolean(
      base::StrCat({kOmniboxAimEntrypointActivatedViaKeyboard,
                    ".ByPageContext.", page_context}),
      via_keyboard);
 } 
 >>> 
 ... 
```
### patch
```cpp

bool OmniboxEditModel::CanPasteAndGo(const std::u16string& text) const {
#if BUILDFLAG(ENABLE_COMMANDER)
  if (base::FeatureList::IsEnabled(features::kBraveCommander) &&
      text.starts_with(commander::kCommandPrefix)) {
    return false;
  }
#endif
  return CanPasteAndGo_Chromium(text);
}

void OmniboxEditModel::PasteAndGo(const std::u16string& text,
                                  base::TimeTicks match_selection_timestamp) {
  if (view_) {
    view_->RevertAll();
  }

  PasteAndGo_Chromium(text, match_selection_timestamp);
}

// Chromium dynamically updates search engine's favicon when the user visits the
// search engine (see SearchEngineTabHelper::OnFaviconUpdated). However, Google
// search has different favicons for regular search vs shopping search. Because
// of this, if Google is the default search engine the omnibox would switch
// between the two favicons depending on which search was used last. To avoid
// this Chrome uses prepackaged icons returned by the method below. We don't
// have the same icons since those are Chrome specific, so we are going to use a
// generic Google color icon here for both light and dark modes.
ui::ImageModel OmniboxEditModel::GetSuperGIcon(int image_size,
                                               bool dark_mode) const {
  return ui::ImageModel::FromVectorIcon(vector_icons::kGoogleColorIcon,
                                        gfx::kPlaceholderColor, image_size);
}
```

