### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/attribution_reporting/aggregatable_trigger_config.h"

 ... 
```
### patch
```cpp
#include "components/attribution_reporting/aggregatable_trigger_config.h"

```

### match
```cpp
...
 
 namespace attribution_reporting { ...   >>> 
 std::optional<AggregatableTriggerConfig> 
 AggregatableTriggerConfig::Create 
 (  <<< 
SourceRegistrationTimeConfig source_registration_time_config
 ... ) ...  } ...  
```
### patch
```cpp
std::optional<AggregatableTriggerConfig> AggregatableTriggerConfig::Create_Unused(

```

### match
```cpp
...
 
 namespace attribution_reporting { ... 
 
 bool AggregatableTriggerConfig::ShouldCauseAReportToBeSentUnconditionally()
    const { ... 
return trigger_context_id_.has_value() ||
         !aggregatable_filtering_id_max_bytes_.IsDefault();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace attribution_reporting {
std::optional<AggregatableTriggerConfig> AggregatableTriggerConfig::Create(
    SourceRegistrationTimeConfig source_registration_time_config,
    std::optional<std::string> trigger_context_id,
    AggregatableFilteringIdsMaxBytes max_bytes) {
  return std::nullopt;
}

```

