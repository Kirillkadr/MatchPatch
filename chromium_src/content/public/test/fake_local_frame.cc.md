### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "content/public/test/fake_local_frame.h"

 ... 
```
### patch
```cpp
#include "content/public/test/fake_local_frame.h"

```

### match
```cpp
...
 
 namespace content { ... 
void FakeLocalFrame::PerformFullContentSpellCheck() {}
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
void FakeLocalFrame::GetImageAt(const ::gfx::Point& window_point,
                                GetImageAtCallback callback) {
  std::move(callback).Run(SkBitmap());
}

```

