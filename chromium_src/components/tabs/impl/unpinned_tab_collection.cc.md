### match
```cpp
...
// found in the LICENSE file.
 #include "components/tabs/public/unpinned_tab_collection.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "components/tabs/public/tab_collection.h"

```

### match
```cpp
...
 /*supports_tabs=*/ 
 true 
 ) 
 {} 
 >>> 
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_ANDROID)
UnpinnedTabCollection::UnpinnedTabCollection()
    : TabCollection(TabCollection::Type::UNPINNED,
                    {TabCollection::Type::GROUP, TabCollection::Type::SPLIT, TabCollection::Type::TREE_NODE},
                    /*supports_tabs=*/true) {}
#endif  // !BUILDFLAG(IS_ANDROID)

```

