### match
```cpp
...
// found in the LICENSE file.
 #include "components/heap_profiling/in_process/heap_profiler_parameters.h"
 
 >>> 
#include "base/check_op.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 namespace 
 heap_profiling 
 { 
 >>> 
namespace {
...
}
 ... 
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kHeapProfilerReporting, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

