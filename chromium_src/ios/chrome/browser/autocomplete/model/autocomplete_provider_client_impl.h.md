### match
```
...
 
 # ifndef ... 
 #define IOS_CHROME_BROWSER_AUTOCOMPLETE_MODEL_AUTOCOMPLETE_PROVIDER_CLIENT_IMPL_H_
 
 >>> 
#import "base/memory/raw_ptr.h"

 ... 
```
### patch
```
#include "build/build_config.h"
#include "components/omnibox/browser/autocomplete_provider_client.h"

```

### match
```
...
 
 # ifndef ... 
const AutocompleteSchemeClassifier& GetSchemeClassifier() const override;
 AutocompleteClassifier* GetAutocompleteClassifier() override; 
 >>> 
history::HistoryService* GetHistoryService() override;
 ... 
```
### patch
```
  void OpenLeo(const std::u16string& query) override; 
  bool IsLeoProviderEnabled() override;

```

