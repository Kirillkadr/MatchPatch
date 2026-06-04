### match
```cpp
...
#include <string>

 #include <string_view>
 
 >>> 
#include "base/base64.h"

 ... 
```
### patch
```cpp
#include <string>
#include "brave/components/omnibox/browser/brave_search_suggestion_parser.h"
#include "components/omnibox/browser/autocomplete_match_type.h"
#include "third_party/omnibox_proto/types.pb.h"

```

### match
```cpp
...
", 1), i++) {
    // Remove any XSSI guards to allow for JSON parsing.
    json_data.remove_prefix(response_start_index);

    std::optional<base::Value> data =
        base::JSONReader::Read(json_data, base::JSON_ALLOW_TRAILING_COMMAS);
    if (data && data->is_list()) {
      return std::move(data->GetList());
    }
  }
  return std::nullopt;
}

// static
  >>> 
 bool 
 SearchSuggestionParser::ParseSuggestResults 
 (  <<< 
const base::ListValue& root_list
 ... ) ...  
```
### patch
```cpp
bool SearchSuggestionParser::ParseSuggestResults_Chromium(

```

### match
```cpp
...
>>>
 bool 
 SearchSuggestionParser::ParseSuggestResults 
 (  <<< 
const base::ListValue& root_list
 ... ) ...  
```
### patch
```cpp
bool SearchSuggestionParser::ParseSuggestResults_Chromium(

```

### match
```cpp
...
 
 bool SearchSuggestionParser::ParseSuggestResults_Chromium(
const base::ListValue& root_list,
    const AutocompleteInput& input,
    const AutocompleteSchemeClassifier& scheme_classifier,
    int default_result_relevance,
    bool is_keyword_result,
    Results* results) { ...   >>> 
 return 
 SearchSuggestionParser::ParseSuggestResults 
 (  <<<  ...) ...  } ...  
```
### patch
```cpp
  return SearchSuggestionParser::ParseSuggestResults_Chromium(

```

### match
```cpp
...
 
 bool SearchSuggestionParser::ParseSuggestResults_Chromium(
const base::ListValue& root_list,
    const AutocompleteInput& input,
    const AutocompleteSchemeClassifier& scheme_classifier,
    int default_result_relevance,
    bool is_keyword_result,
    Results* results) { ... 
return SearchSuggestionParser::ParseSuggestResults_Chromium(
			root_list, input, scheme_classifier, default_result_relevance,
      is_keyword_result,
      /*options=*/{}, results);
 } 
 >>> 
 ... 
```
### patch
```cpp
// static
bool SearchSuggestionParser::ParseSuggestResults(
    const base::ListValue& root_list,
    const AutocompleteInput& input,
    const AutocompleteSchemeClassifier& scheme_classifier,
    int default_result_relevance,
    bool is_keyword_result,
    const ParseSuggestResultsOptions& options,
    Results* results,
    bool is_brave_rich_suggestion) {
  if (is_brave_rich_suggestion) {
    return omnibox::ParseSuggestResults(root_list, input, is_keyword_result,
                                        results);
  }
  return SearchSuggestionParser::ParseSuggestResults_Chromium(
      root_list, input, scheme_classifier, default_result_relevance,
      is_keyword_result, options, results);
}

// static
bool SearchSuggestionParser::ParseSuggestResults(
    const base::ListValue& root_list,
    const AutocompleteInput& input,
    const AutocompleteSchemeClassifier& scheme_classifier,
    int default_result_relevance,
    bool is_keyword_result,
    Results* results,
    bool is_brave_rich_suggestion) {
  return SearchSuggestionParser::ParseSuggestResults(
      root_list, input, scheme_classifier, default_result_relevance,
      is_keyword_result,
      /*options=*/{}, results, is_brave_rich_suggestion);
}
```

