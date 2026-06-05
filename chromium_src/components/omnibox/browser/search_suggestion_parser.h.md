### match
```cpp
...
>>> 
static bool ParseSuggestResults(
      const base::ListValue& root_list,
      const AutocompleteInput& input,
      const AutocompleteSchemeClassifier& scheme_classifier,
      int default_result_relevance,
      bool is_keyword_result,
      const ParseSuggestResultsOptions& options,
      Results* results);

  // ParseSuggestResultsWithOptions with optional values set to their default
  static bool ParseSuggestResults(
      const base::ListValue& root_list,
      const AutocompleteInput& input,
      const AutocompleteSchemeClassifier& scheme_classifier,
      int default_result_relevance,
      bool is_keyword_result,
      Results* results);
<<< 
 ...
```
### patch
```cpp
static bool ParseSuggestResults_Chromium(
      const base::ListValue& root_list,
      const AutocompleteInput& input,
      const AutocompleteSchemeClassifier& scheme_classifier,
      int default_result_relevance,
      bool is_keyword_result,
      const ParseSuggestResultsOptions& options,
      Results* results);
  static bool ParseSuggestResults(
      const base::ListValue& root_list,
      const AutocompleteInput& input,
      const AutocompleteSchemeClassifier& scheme_classifier,
      int default_result_relevance,
      bool is_keyword_result,
      const ParseSuggestResultsOptions& options,
      Results* results,bool is_brave_rich_suggestion = false);

  // ParseSuggestResultsWithOptions with optional values set to their default
  static bool ParseSuggestResults_Chromium(
      const base::ListValue& root_list,
      const AutocompleteInput& input,
      const AutocompleteSchemeClassifier& scheme_classifier,
      int default_result_relevance,
      bool is_keyword_result,
      Results* results);
  static bool ParseSuggestResults(
      const base::ListValue& root_list,
      const AutocompleteInput& input,
      const AutocompleteSchemeClassifier& scheme_classifier,
      int default_result_relevance,
      bool is_keyword_result,
      Results* results,bool is_brave_rich_suggestion = false);

```

