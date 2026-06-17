### match
```cpp
...
 #include "ui/gfx/native_ui_types.h"
 
 >>> 
 ... 
```
### patch
```cpp
class SplitViewCommonBrowserTest;

```

### match
```cpp
...
 
 namespace web_modal { ... 
// Focus the topmost modal dialog.  IsDialogActive() must be true when calling
 // this function. 
 >>> 
 ... } ...  
```
### patch
```cpp
  void OnTabActiveStateChanged();                 
  friend class ::SplitViewCommonBrowserTest;

```

