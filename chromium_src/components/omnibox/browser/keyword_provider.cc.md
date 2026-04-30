### match
```cpp
...
#include <utility>

 #include <vector>
 
 >>> 
#include "base/memory/raw_ptr.h"

 ... 
```
### patch
```cpp
#include "components/omnibox/browser/autocomplete_match.h"
#include "components/search_engines/template_url.h"
#include "components/search_engines/template_url_starter_pack_data.h"

```

### match
```cpp
...
 
 void KeywordProvider::FillInUrlAndContents(
    const std::u16string& remaining_input,
    const TemplateURL* turl,
    AutocompleteMatch* match) const { ... 
 if ( ... 
turl->starter_pack_id() ==
          >>> 
 template_url_starter_pack_data::StarterPackId::kAiMode 
 ) 
 {  <<< 
match->contents.assign(
          l10n_util::GetStringUTF16(IDS_EMPTY_STARTER_PACK_AI_MODE_VALUE));
 ... } ...  } ...  
```
### patch
```cpp
        template_url_starter_pack_data::StarterPackId::kAiMode || turl->starter_pack_id() == 
                 template_url_starter_pack_data::kAskBraveSearch) {

```

