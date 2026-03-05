### match
```
...
#include <memory>

 #include <utility>
 
 >>> 
#include "base/trace_event/trace_event.h"

 ... 
```
### patch
```
#include "third_party/abseil-cpp/absl/container/internal/layout.h"
#include "third_party/blink/renderer/core/timing/time_clamper.h"

```

### match
```
...
 namespace blink { ... 
 double VideoFrameCallbackRequesterImpl::GetCoarseClampedTimeInSeconds(
    base::TimeDelta time) { ...   >>> 
 base::Microseconds(TimeClamper::kCoarseResolutionMicroseconds) 
 ,  <<< ... 
"kCoarseResolution should be at least as coarse as other clock "
      "resolutions"
 ... } ...  } ...  
```
### patch
```
          base::Microseconds(TimeClamper::kCoarseResolutionMicroseconds_ChromiumImpl),

```

### match
```
...
 namespace blink { ... 
 double VideoFrameCallbackRequesterImpl::GetCoarseClampedTimeInSeconds(
    base::TimeDelta time) { ... 
static_assert(
      kCoarseResolution >=
                    base::Microseconds(TimeClamper::kCoarseResolutionMicroseconds_ChromiumImpl),
		"kCoarseResolution should be at least as coarse as other clock "
      "resolutions");  >>> 
 return time.FloorToMultiple(kCoarseResolution).InSecondsF();  <<< ... } ...  } ...  
```
### patch
```
  return time.FloorToMultiple(
      base::Microseconds(TimeClamper::CoarseResolutionMicroseconds())).InSecondsF();

```

