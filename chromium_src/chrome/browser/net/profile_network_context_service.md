### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/net/profile_network_context_service.h"

 ... 
```
### patch
```cpp
static const char* kBraveCTExcludedHosts[] = {
    // Critical endpoints that shouldn't require SCTs so they always work
    "updates.bravesoftware.com",
    "updates-cdn.bravesoftware.com",
    "usage-ping.brave.com",
    // Test host for manual testing
    "sct-exempted.bravesoftware.com",
};

#define BRAVE_PROFILE_NETWORK_CONTEXT_SERVICE_GET_CT_POLICY \
  for (const auto* host : kBraveCTExcludedHosts) {          \
    excluded.push_back(host);                               \
  }

```

### match
```cpp
...
 
 void ProfileNetworkContextService::Shutdown() { ... 
profile_ = nullptr;
 } 
 >>> 
 ... 
```
### patch
```cpp
#undef BRAVE_PROFILE_NETWORK_CONTEXT_SERVICE_GET_CT_POLICY
```

