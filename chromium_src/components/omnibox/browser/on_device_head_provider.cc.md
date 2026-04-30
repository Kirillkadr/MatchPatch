### match
```cpp
...
#include "third_party/metrics_proto/omnibox_focus_type.pb.h"

 #include "third_party/metrics_proto/omnibox_input_type.pb.h"
 
 >>> 
namespace {
const int kBaseRelevanceForUrlInput = 99;
const int kTailBaseRelevance = 90;
const size_t kMaxRequestId = std::numeric_limits<size_t>::max() - 1;

int OnDeviceHeadSuggestMaxScoreForNonUrlInput(bool is_incognito) {
  const int kDefaultScore =
#if BUILDFLAG(IS_IOS)
      99;
#else
      is_incognito ? 99 : 1000;
#endif  // BUILDFLAG(IS_IOS)
  return kDefaultScore;
}

std::string SanitizeInput(const std::u16string& input) {
  std::u16string trimmed_input;
  base::TrimWhitespace(input, base::TRIM_ALL, &trimmed_input);
  return base::UTF16ToUTF8(base::i18n::ToLower(trimmed_input));
}

enum class SuggestionType {
  HEAD = 0,
  TAIL,
};

struct Suggestion {
  std::string text;
  SuggestionType type;

  Suggestion(std::string text, SuggestionType type) : text(text), type(type) {}
};

}
 ... 
```
### patch
```cpp
#include "components/search/search.h"
#include "components/search_engines/template_url_service.h"
namespace search {
bool BraveEnableOnHeadDeviceForAnyProvider(
    const TemplateURLService* template_url_service) {
  return true;
}
}  // namespace search

```

### match
```cpp
...
 
 bool OnDeviceHeadProvider::IsOnDeviceHeadProviderAllowed(
    const AutocompleteInput& input) { ...   >>> 
 if 
 (!client()->SearchSuggestEnabled())  <<< 
return false;
 ... } ...  
```
### patch
```cpp
  if (!client()->SearchSuggestEnabled() && false)

```

### match
```cpp
...
 
 bool OnDeviceHeadProvider::IsOnDeviceHeadProviderAllowed(
    const AutocompleteInput& input) { ...   >>> 
 return 
 search::DefaultSearchProviderIsGoogle 
 (  <<< 
client()->GetTemplateURLService()
 ... ) ...  } ...  
```
### patch
```cpp
  return search::BraveEnableOnHeadDeviceForAnyProvider(

```

### match
```cpp
...
 
 void OnDeviceHeadProvider::AllSearchDone(
    std::unique_ptr<OnDeviceHeadProviderParams> params) { ...   >>> 
 if 
 (search::DefaultSearchProviderIsGoogle(template_url_service)) 
 {  <<< 
matches_.clear();
 ... } ...  } ...  
```
### patch
```cpp
  if (search::BraveEnableOnHeadDeviceForAnyProvider(template_url_service)){

```

