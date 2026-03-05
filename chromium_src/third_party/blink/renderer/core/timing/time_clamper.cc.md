### match
```
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "third_party/blink/renderer/core/timing/time_clamper.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/timing/time_clamper.h"

```

### match
```
...
#include "third_party/blink/renderer/core/timing/time_clamper.h"

 #include "third_party/blink/renderer/core/timing/time_clamper.h"
 
 >>> 
#include "base/bit_cast.h"

 ... 
```
### patch
```
#include "base/feature_list.h"
#include "base/time/time.h"
#include "third_party/blink/public/common/features.h"

```

### match
```
...
>>>
 ? 
 kFineResolutionMicroseconds 
 : 
 kCoarseResolutionMicroseconds 
 ;  <<< ... 
```
### patch
```
                       ? FineResolutionMicroseconds()
                       : CoarseResolutionMicroseconds();

```
### match
```
...
namespace blink {
...
>>>
}

```
### patch
```
namespace {

constexpr int kBraveTimerResolutionMicroseconds = 1000;

bool ShouldRound() {
  return base::FeatureList::IsEnabled(features::kBraveRoundTimeStamps);
}

}  // namespace

// static
double TimeClamper::MaybeRoundMilliseconds(double value) {
  return ShouldRound() ? round(value) : value;
}

// static
base::TimeDelta TimeClamper::MaybeRoundTimeDelta(base::TimeDelta value) {
  return ShouldRound() ? value.RoundToMultiple(base::Microseconds(
                             kBraveTimerResolutionMicroseconds))
                       : value;
}

// static
int TimeClamper::FineResolutionMicroseconds() {
  return ShouldRound() ? kBraveTimerResolutionMicroseconds
                       : kFineResolutionMicroseconds_ChromiumImpl;
}

// static
int TimeClamper::CoarseResolutionMicroseconds() {
  return ShouldRound() ? kBraveTimerResolutionMicroseconds
                       : kCoarseResolutionMicroseconds_ChromiumImpl;
}
```
