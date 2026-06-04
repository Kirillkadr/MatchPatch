### match
```cpp
...
 
 # ifndef ... 
#include <string>

 #include <string_view>
 
 >>> 
#include "base/containers/flat_set.h"

 ... 
```
### patch
```cpp
#include <string>

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace password_manager { ... 
 base::flat_set<std::u16string> passwords 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  int GetPasswordStrength(const std::string& password)
// Returns strength for `password` on a scale from 0 to 100.;

```

