### match
```cpp
...
#include "base/types/to_address.h"

 #include "base/uuid.h"
 
 >>> 
#include "chrome/browser/profiles/profile.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/views/bookmarks/saved_tab_groups/brave_saved_tab_group_button.h"

```

### match
```cpp
...
 
 AddChildViewAt ( ... 
>>> 
 std::make_unique<SavedTabGroupButton> 
 ( 
<<< 
...) ...  ) ...  
```
### patch
```cpp
      std::make_unique<BraveSavedTabGroupButton>(

```

### match
```cpp
...
 
 AddChildViewAt ( ... 
 
 std::make_unique<BraveSavedTabGroupButton> ( ... 
 
 base::BindRepeating ( ... 
>>> 
 weak_ptr_factory_.GetWeakPtr() 
 , 
 group.saved_guid() 
 ) 
 , 
<<< 
browser_->GetBrowserForMigrationOnly()
 ... ) ...  ) ...  
```
### patch
```cpp
                              base::Unretained(this), group.saved_guid()), 

```

