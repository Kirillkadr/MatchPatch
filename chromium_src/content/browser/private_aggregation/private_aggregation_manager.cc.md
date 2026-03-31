### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "content/browser/private_aggregation/private_aggregation_manager.h"

 ... 
```
### patch
```cpp
#include "content/browser/private_aggregation/private_aggregation_manager.h"

```

### match
```cpp
...
 
 namespace content { ...   >>> 
 PrivateAggregationManager 
 * 
 PrivateAggregationManager::GetManager 
 (  <<< 
BrowserContext& browser_context
 ... ) ...  } ...  
```
### patch
```cpp
PrivateAggregationManager* PrivateAggregationManager::GetManager_ChromiumImpl(

```

### match
```cpp
...
 
 namespace content { ... 
 
 bool PrivateAggregationManager::ShouldSendReportDeterministically(
    PrivateAggregationCallerApi caller_api,
    const std::optional<std::string>& context_id,
    base::StrictNumeric<size_t> filtering_id_max_bytes,
    std::optional<size_t> requested_max_contributions) { ... 
return false;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
PrivateAggregationManager* PrivateAggregationManager::GetManager(
    BrowserContext& browser_context) {
  return nullptr;
}

```

