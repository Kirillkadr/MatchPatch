### match
```cpp
...
#include <memory>

 #include <string>
 
 >>> 
#include "components/sessions/content/extended_info_handler.h"

 ... 
```
### patch
```cpp
#include <string>
#include "components/sessions/core/serialized_navigation_driver.h"
#include "components/sessions/core/serialized_navigation_entry.h"

```

### match
```cpp
...
 
 namespace sessions { ... 
 
 class SESSIONS_EXPORT ContentSerializedNavigationDriver
    : public SerializedNavigationDriver { ... 
// SerializedNavigationDriver implementation.
 int GetDefaultReferrerPolicy() const override; 
 >>> 
std::string GetSanitizedPageStateForPickle(
      const SerializedNavigationEntry* navigation) const override;
 ... } ...  } ...  
```
### patch
```cpp
  std::string GetSanitizedPageStateForPickle_ChromiumImpl(
      const SerializedNavigationEntry* navigation) const; 

```

