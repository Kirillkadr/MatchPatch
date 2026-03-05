### match
```
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "third_party/blink/renderer/platform/loader/fetch/https_state.h"

 ... 
```
### patch
```
#include <optional>
#include "third_party/blink/renderer/platform/loader/fetch/https_state.h"

```

### match
```
...
>>>
 HttpsState 
 CalculateHttpsState 
 ( 
 const SecurityOrigin* security_origin 
 ,  <<< ... 
std::optional<HttpsState> parent_https_state
 ... ) ...  
```
### patch
```
HttpsState CalculateHttpsState_ChromiumImpl(const SecurityOrigin* security_origin,

```

### match
```
...
 namespace blink { ... 
 HttpsState CalculateHttpsState_ChromiumImpl(const SecurityOrigin* security_origin,
std::optional<HttpsState> parent_https_state) { ... 
return HttpsState::kNone;
 } 
 >>> 
 ... } ...  
```
### patch
```
HttpsState CalculateHttpsState(const SecurityOrigin* security_origin,
                               std::optional<HttpsState> parent_https_state) {
  if (security_origin && (security_origin->Protocol() == "http" &&
                          security_origin->Host().EndsWith(".onion"))) {
    // MixedContentChecker::ShouldAutoupgrade upgrades resource only on the
    // kModern pages. Return it for .onion as for https.
    return HttpsState::kModern;
  }
  return CalculateHttpsState_ChromiumImpl(security_origin, parent_https_state);
}

```

