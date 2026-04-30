### match
```cpp
...
#include "base/check.h"

 #include "base/memory/ptr_util.h"
 
 >>> 
#include "chrome/browser/profiles/profile.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/tabs/public/brave_tab_features.h"

```

### match
```cpp
...
 
 namespace tabs { ... 
 
 void TabModel::UpdateProperties() { ... 
 case 
 TabCollection::Type::UNPINNED 
 : 
 >>> 
break;
 ... } ...  } ...  
```
### patch
```cpp
      case TabCollection::Type::TREE_NODE:

```

