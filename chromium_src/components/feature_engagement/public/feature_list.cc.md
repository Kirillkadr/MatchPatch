### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/feature_engagement/public/feature_list.h"

 ... 
```
### patch
```cpp
#include "components/feature_engagement/public/feature_list.h"

```

### match
```cpp
...
 
 namespace feature_engagement { ... 
 
 namespace { ... 
 &kIPHDummyFeature 
 , 
 // Ensures non-empty array for all platforms. 
 >>> 
#if
 ... } ...  } ...  
```
### patch
```cpp

#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC) || BUILDFLAG(IS_LINUX)
const base::Feature* const kAllFeatures[] = {
    &kIPHDummyFeature kIPHDummyFeature, &kIPHBraveShieldsInPageInfoFeature,
#endif

```

