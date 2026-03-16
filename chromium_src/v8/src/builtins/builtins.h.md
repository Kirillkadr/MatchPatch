### match
```cpp

>>>
...
```

### patch

```cpp

#include "brave/components/brave_page_graph/common/buildflags.h"
```
### match
```cpp

...
namespace v8 {
...
namespace internal {
...
>>>
}
...
}
...
```

### patch
```cpp

#if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH_WEBAPI_PROBES)
class BuiltinArguments;
void ReportBuiltinCallAndResponse(Isolate* isolate,
                                  const char* builtin_name,
                                  const BuiltinArguments& builtin_args,
                                  const Tagged<Object>& builtin_result);
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH_WEBAPI_PROBES)
```

