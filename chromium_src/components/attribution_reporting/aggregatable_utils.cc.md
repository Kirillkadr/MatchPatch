### match
```cpp
...
#include <optional>

 #include <vector>
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```cpp
#include <optional>
#include "components/attribution_reporting/aggregatable_utils.h"

```

### match
```cpp
...
>>>
 std::vector<NullAggregatableReport> 
 GetNullAggregatableReports 
 (  <<< 
const AggregatableTriggerConfig& config
 ... ) ...  
```
### patch
```cpp
std::vector<NullAggregatableReport> GetNullAggregatableReports_ChromiumImpl(

```

### match
```cpp
...
 
 namespace attribution_reporting { ... 
 
 bool IsAggregatableBudgetInRange(int budget) { ... 
return budget >= 0 && budget <= kMaxAggregatableValue;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
std::vector<NullAggregatableReport> GetNullAggregatableReports(
    const AggregatableTriggerConfig&,
    base::Time trigger_time,
    std::optional<base::Time> attributed_source_time,
    GenerateNullAggregatableReportFunc) {
  return {};
}

```

