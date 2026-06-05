### match
```cpp
...
 #include "components/omnibox/common/omnibox_features.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "components/search_engines/template_url.h"

```

### match
```cpp
...
 #include "ui/views/property_effects.h"
 
 >>> 
// static
 ... 
```
### patch
```cpp
const gfx::VectorIcon& GetAskBraveSearchStarterPackIcon();


```

### match
```cpp
...
 
 void SelectedKeywordView::SetCustomImage(const gfx::Image& image) { ... 
 if ( ... 
>>> 
 template_url_starter_pack_data::StarterPackId::kAiMode 
 ) 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
                 template_url_starter_pack_data::StarterPackId::kAskBraveSearch) {
    vector_icon = &GetAskBraveSearchStarterPackIcon();
    /* NOLINTNEXTLINE */
  } else if (template_url && template_url->starter_pack_id() == 
                                 template_url_starter_pack_data::kAiMode) {

```

