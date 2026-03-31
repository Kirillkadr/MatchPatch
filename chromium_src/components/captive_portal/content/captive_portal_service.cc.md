### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/captive_portal/content/captive_portal_service.h"

 ... 
```
### patch
```cpp
#include "components/captive_portal/content/captive_portal_service.h"

```

### match
```cpp
...
 
 namespace captive_portal { ... 
 
 void CaptivePortalService::UpdateEnabledState() { ... 
bool enabled_before = enabled_;  >>> 
 enabled_ = testing_state_ != DISABLED_FOR_TESTING &&
             resolve_errors_with_web_service_.GetValue();  <<< 
if (enabled_before == enabled_)
    return;
 ... } ...  } ...  
```
### patch
```cpp
  enabled_ = testing_state_ != DISABLED_FOR_TESTING;
  true && resolve_errors_with_web_service_.GetValue();

```

