### match
```
...
#include <string>

 #include <vector>
 
 >>> 
#include "base/android/device_info.h"

 ...
```
### patch
```
#include "base/strings/strcat.h"
#include "base/system/sys_info.h"

```

### match
```
...
#include <sys/utsname.h>

 #endif 
 >>> 
 ...
```
### patch
```
namespace {
constexpr char kBraveBrandNameForCHUA[] = "Brave";

}  // namespace

```

### match
```
...
 namespace 
 embedder_support 
 { 
 >>> 
namespace {

 ...
```
### patch
```
std::string BuildModelInfo_ChromiumImpl();
std::string BuildModelInfo() {
  return std::string();
}

```

### match
```
...
 
 namespace embedder_support { ... 
 
 namespace { ... 
 
 const blink::UserAgentBrandList GetUserAgentBrandList(
    const std::string& major_version,
    const std::string& full_version,
    blink::UserAgentBrandVersionType output_version_type,
    std::optional<blink::UserAgentBrandVersion> additional_brand_version) { ... 
brand = version_info::GetProductName();
 #endif 
 >>> 
 ... } ...  } ...  } ...  
```
### patch
```
brand = kBraveBrandNameForCHUA;

```

### match
```
...
output_version_type == blink::UserAgentBrandVersionType::kFullVersion  >>> 
 ? 
 full_version  <<<  ...
```
### patch
```
          base::StrCat({major_version, ".0.0.0"})

```

### match
```
...
 
 namespace embedder_support { ... 
 
 namespace { ... 
 
 const blink::UserAgentBrandList GetUserAgentBrandList(
    const std::string& major_version,
    const std::string& full_version,
    blink::UserAgentBrandVersionType output_version_type,
    std::optional<blink::UserAgentBrandVersion> additional_brand_version) { ... 
output_version_type == blink::UserAgentBrandVersionType::kFullVersion  >>> 
 ? 
 base::StrCat({major_version, ".0.0.0"})  <<<  ...} ...  } ...  } ...  
```
### patch
```
          base::StrCat({major_version, ".0.0.0"})

```
