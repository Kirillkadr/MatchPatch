### match
```cpp
...
#include <optional>

 #include <string>
 
 >>> 
#include "chrome/browser/ui/tabs/existing_base_sub_menu_model.h"

 ... 
```
### patch
```cpp
#include "base/gtest_prod_util.h"

```

### match
```cpp
...
 
 class SplitTabMenuModel : public ui::SimpleMenuModel,
                          public ui::SimpleMenuModel::Delegate { ... 
 kExitSplit 
 , 
 >>> 
kSendFeedback
 ... } ...  
```
### patch
```cpp
    kToggleLinkState,

```

### match
```cpp
...
 
 class SplitTabMenuModel : public ui::SimpleMenuModel,
                          public ui::SimpleMenuModel::Delegate { ...   >>> 
 const 
 gfx::VectorIcon 
 & 
 GetReversePositionIcon 
 (  <<< 
split_tabs::SplitTabActiveLocation active_split_tab_location
 ... ) ...  } ...  
```
### patch
```cpp
  virtual const gfx::VectorIcon& GetReversePositionIcon(

```

### match
```cpp
...
split_tabs::SplitTabLayout GetSplitLayout() const;
 void CloseTabAtIndex(int index); 
 >>> 
void SendFeedback();
 ... 
```
### patch
```cpp
  friend class BraveSplitTabMenuModel;
  FRIEND_TEST_ALL_PREFIXES(BraveTabMenuBrowserTest,
                           SplitViewMenuCustomizationTest);
  static CommandId GetCommandIdEnum(int command_id);
  static int GetCommandIdInt(CommandId command_id);

```

