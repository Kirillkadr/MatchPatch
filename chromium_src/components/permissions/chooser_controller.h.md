### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <vector>
 
 >>> 
#include "base/memory/raw_ptr.h"

 ... 
```
### patch
```cpp
#include <optional>

```

### match
```cpp
...
 
 # ifndef ... 
 namespace 
 permissions 
 { 
 >>> 
// Subclass ChooserController to implement a chooser, which has some
 ... } ...  
```
### patch
```cpp
enum class ChooserControllerType {
  kBluetooth,
};

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
// Returns the label for SelectAll checkbox.
 virtual std::u16string GetSelectAllCheckboxLabel() const; 
 >>> 
// Returns the label for the throbber shown while options are initializing or
 ... } ...  
```
### patch
```cpp
  virtual std::optional<ChooserControllerType> GetType() const;

```

