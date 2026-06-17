### match
```cpp
...
// found in the LICENSE file.
 #include "components/user_data_importer/content/content_bookmark_parser.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include <optional>
#include <vector>
#include "base/containers/span.h"
#include "build/build_config.h"

```

### match
```cpp
...
 #include "content/public/browser/service_process_host.h"
 
 >>> 
 ... 
```
### patch
```cpp
#if BUILDFLAG(IS_ANDROID)
namespace importer {
std::optional<std::vector<uint8_t>> ReencodeFavicon(
    base::span<const uint8_t> src) {
  return std::nullopt;
}
}  // namespace importer
#endif

```

