### match
```cpp
...
// found in the LICENSE file.
 #include "components/enterprise/browser/reporting/policy_info.h"
 
 >>> 
#include <string>

 ... 
```
### patch
```cpp
#include "components/policy/core/common/policy_types.h"

```

### match
```cpp
...
 
 namespace enterprise_reporting { ... 
 
 namespace { ... 
 
 em::Policy_PolicySource GetSource(const base::Value& policy) { ... 
 
 case policy : ... 
 return em::Policy_PolicySource_SOURCE_PRIORITY_CLOUD_DEPRECATED; 
 >>> 
 ... } ...  } ...  } ...  
```
### patch
```cpp
    case policy::POLICY_SOURCE_BRAVE:
  return em::Policy_PolicySource_SOURCE_UNKNOWN;

```

