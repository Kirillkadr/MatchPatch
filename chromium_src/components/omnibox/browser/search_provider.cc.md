### match
```cpp
...
// found in the LICENSE file.
 #include "components/omnibox/browser/search_provider.h"
 
 >>> 
#include <stddef.h>

 ... 
```
### patch
```cpp
#include "components/omnibox/browser/search_suggestion_parser.h"
#include "components/search_engines/search_engine_type.h"

```

### match
```cpp
...
 
 if (data) { ... 

          *data, GetInput(is_keyword), client()->GetSchemeClassifier(),
          /*default_result_relevance=*/-1, /*is_keyword_result=*/is_keyword,
            >>> 
 results 
 ) 
 ;  <<<  ...} ...  
```
### patch
```cpp
          results,IsBraveRichSuggestion(is_keyword_result));

```

### match
```cpp
...
 
 void SearchProvider::PrefetchImages(SearchSuggestionParser::Results* results) { ... 
for (const GURL& url : prefetch_image_urls)
    client()->PrefetchImage(url);
 } 
 >>> 
 ... 
```
### patch
```cpp
bool SearchProvider::IsBraveRichSuggestion(bool is_keyword) {
  auto* url = is_keyword ? providers_.GetKeywordProviderURL()
                         : providers_.GetDefaultProviderURL();
  return url && url->GetEngineType(
                    client()->GetTemplateURLService()->search_terms_data()) ==
                    SEARCH_ENGINE_BRAVE;
}

class BraveSearchProvider* SearchProvider::AsBraveSearchProvider() {
  NOTREACHED() << "We replaces SearchProvider with BraveSearchProvider";
}
```

