### match
```cpp
...
// found in the LICENSE file.
 #include "extensions/common/constants.h"
 
 >>> 
#include <string_view>

 ...
```
### patch
```cpp
#include "base/containers/map_util.h"
```

### match
```cpp
...
#include "build/chromecast_buildflags.h"

 #include "build/chromeos_buildflags.h"
 
 >>>  ...
```
### patch
```cpp
namespace extensions_mv2 {
```

### match
```cpp
...
#include "build/chromeos_buildflags.h"

 namespace 
 extensions_mv2 
 { 
 >>> 
...
} ...
```
### patch
```cpp

namespace {

// Checks kBraveHosted and kWebStoreHosted maps are in consistent state at
// compile time. Keys of one map should be the values of another.
consteval bool CheckExtensionMaps() {
  for (const auto& [brave_hosted_key, brave_hosted_value] : kBraveHosted) {
    if (brave_hosted_value.empty()) {
      // skip Brave-hosted extension which doesn't have the WebStore
      // counterpart.
      continue;
    }

    bool ok = false;
    for (const auto& [webstore_hosted_key, webstore_hosted_value] :
         kWebStoreHosted) {
      if (brave_hosted_value == webstore_hosted_key &&
          brave_hosted_key == webstore_hosted_value) {
        ok = true;
        break;
      }
    }
    if (!ok) {
      return false;
    }
  }
  return true;
}

static_assert(CheckExtensionMaps(),
              "kBraveHosted & kWebStoreHosted aren't consistent");
}  // namespace

bool IsKnownBraveHostedExtension(const extensions::ExtensionId& id) {
  return kBraveHosted.contains(id);
}

bool IsKnownWebStoreHostedExtension(const extensions::ExtensionId& id) {
  return kWebStoreHosted.contains(id);
}

std::optional<extensions::ExtensionId> GetBraveHostedExtensionId(
    const extensions::ExtensionId& webstore_extension_id) {
  if (const auto* fnd =
          base::FindOrNull(kWebStoreHosted, webstore_extension_id)) {
    return extensions::ExtensionId(*fnd);
  }
  return std::nullopt;
}

std::optional<extensions::ExtensionId> GetWebStoreHostedExtensionId(
    const extensions::ExtensionId& brave_hosted_extension_id) {
  if (const auto* fnd =
          base::FindOrNull(kBraveHosted, brave_hosted_extension_id)) {
    return extensions::ExtensionId(*fnd);
  }
  return std::nullopt;
}

}  // namespace extensions_mv2
```

