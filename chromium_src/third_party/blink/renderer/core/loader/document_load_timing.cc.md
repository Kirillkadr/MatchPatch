### match
```
...
/*
 * Copyright (C) 2011 Google, Inc. All Rights Reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 * 1. Redistributions of source code must retain the above copyright
 *    notice, this list of conditions and the following disclaimer.
 * 2. Redistributions in binary form must reproduce the above copyright
 *    notice, this list of conditions and the following disclaimer in the
 *    documentation and/or other materials provided with the distribution.
 *
 * THIS SOFTWARE IS PROVIDED BY GOOGLE INC. ``AS IS'' AND ANY
 * EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
 * IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL GOOGLE INC. OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY
 * OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
 * (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
 * OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 #include "third_party/blink/renderer/core/loader/document_load_timing.h"
 
 >>> 
#include "base/memory/scoped_refptr.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/timing/time_clamper.h"

```

### match
```
...
 namespace blink { ...   >>> 
 base::TimeDelta 
 DocumentLoadTiming::MonotonicTimeToZeroBasedDocumentTime 
 (  <<< ... 
base::TimeTicks monotonic_time
 ... ) ...  } ...  
```
### patch
```
base::TimeDelta DocumentLoadTiming::MonotonicTimeToZeroBasedDocumentTime_ChromiumImpl(

```

### match
```
...
 namespace blink { ... 
 void DocumentLoadTiming::SetRandomizedConfidence(
    const std::optional<RandomizedConfidenceValue>& value) { ... 
NotifyDocumentTimingChanged();
 } 
 >>> 
 ... } ...  
```
### patch
```
base::TimeDelta DocumentLoadTiming::MonotonicTimeToZeroBasedDocumentTime(
    base::TimeTicks monotonic_time) const {
  return TimeClamper::MaybeRoundTimeDelta(
      MonotonicTimeToZeroBasedDocumentTime_ChromiumImpl(monotonic_time));
}

```

