### match
```cpp
...
 #include <string_view>
 
 >>> 
 ... 
```
### patch
```cpp
#include <string>
#include "brave/components/version_info/version_info_values.h"

```

### match
```cpp
...
 
 namespace version_info { ... 
>>> 
 constexpr 
 std::string_view 
 GetProductNameAndVersionForUserAgent() 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
constexpr std::string_view GetProductNameAndVersionForUserAgent_Unused() {

```

### match
```cpp
...
 
 namespace version_info { ... 
 
 constexpr std::string_view GetProductNameAndVersionForUserAgent_Unused() { ... 
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
constexpr std::string GetProductNameAndVersionForUserAgent() {
  return "Chrome/" + std::string(constants::kBraveChromiumVersion);
}

```

