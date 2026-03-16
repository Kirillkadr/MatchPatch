### match
```
...
#include "chrome/browser/autocomplete/autocomplete_classifier_factory.h"

 #include <memory>
 
 >>> 
#include "chrome/browser/autocomplete/chrome_autocomplete_provider_client.h"

 ... 
```
### patch
```
#include "brave/browser/autocomplete/brave_autocomplete_scheme_classifier.h"

```

### match
```
...
 std::unique_ptr<KeyedService> AutocompleteClassifierFactory::BuildInstanceFor(
    content::BrowserContext* context) { ... 
 std::make_unique<AutocompleteClassifier> ( ...   >>> 
 std::make_unique<ChromeAutocompleteSchemeClassifier>(profile) 
 ) 
 ;  <<< ... } ...  
```
### patch
```
      std::make_unique<BraveAutocompleteSchemeClassifier>(profile));

```

