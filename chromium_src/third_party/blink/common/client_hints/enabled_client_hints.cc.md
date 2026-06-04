### match
```cpp
...
// found in the LICENSE file.
 #include "third_party/blink/public/common/client_hints/enabled_client_hints.h"
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include "third_party/blink/public/common/client_hints/enabled_client_hints.h"
#include "third_party/blink/public/common/features.h"

```

### match
```cpp
...
 
 namespace blink { ...   >>> 
 void 
 EnabledClientHints::SetIsEnabled 
 ( 
 const WebClientHintsType type 
 ,  <<< 
const bool should_send
 ... ) ...  } ...  
```
### patch
```cpp
void EnabledClientHints::SetIsEnabled_ChromiumImpl(const WebClientHintsType type,

```

### match
```cpp
...
 
 namespace blink { ... 
std::vector<WebClientHintsType> EnabledClientHints::GetEnabledHints() const {
  std::vector<WebClientHintsType> hints;
  for (const auto& elem : network::GetClientHintToNameMap()) {
    const auto& type = elem.first;
    if (IsEnabled(type))
      hints.push_back(type);
  }
  return hints;
}
 } 
 // namespace blink 
 >>> 
 ... 
```
### patch
```cpp
namespace blink {

void EnabledClientHints::SetIsEnabled(const WebClientHintsType type,
                                      const bool should_send) {
  bool type_is_enabled = false;
  switch (type) {
    case WebClientHintsType::kUA:
    case WebClientHintsType::kUAArch:
    case WebClientHintsType::kUABitness:
    case WebClientHintsType::kUAFullVersionList:
    case WebClientHintsType::kUAMobile:
    case WebClientHintsType::kUAModel:
    case WebClientHintsType::kUAPlatform:
    case WebClientHintsType::kUAPlatformVersion:
    case WebClientHintsType::kUAWoW64:
      type_is_enabled = true;
      break;
    default:
      break;
  }

  if (type_is_enabled) {
    SetIsEnabled_ChromiumImpl(type, should_send);
  } else {
    enabled_types_[static_cast<int>(type)] = false;
  }
}

}  // namespace blink
```

