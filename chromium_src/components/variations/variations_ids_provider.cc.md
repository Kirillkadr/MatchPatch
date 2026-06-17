### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ... 
```
### patch
```cpp
#include "components/variations/variations_ids_provider.h"

```

### match
```cpp
...
 
 namespace variations { ... 
>>> 
 VariationsIdsProvider::GetClientDataHeaders(bool is_signed_in) 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
VariationsIdsProvider::GetClientDataHeaders_Chromium(bool is_signed_in) {

```

