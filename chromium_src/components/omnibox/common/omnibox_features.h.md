### match
```cpp
...
#include "base/feature_list.h"

 #include "base/metrics/field_trial_params.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/feature_list.h"

```

### match
```cpp
...
BASE_DECLARE_FEATURE(kImageSearchSuggestionThumbnail);
 BASE_DECLARE_FEATURE(kOmniboxRemoveSuggestionsFromClipboard); 
 >>> 
// Features that affect the "twiddle" step of AutocompleteController, e.g.,
 ... 
```
### patch
```cpp
BASE_DECLARE_FEATURE(kOmniboxTabSwitchByDefault);

```

