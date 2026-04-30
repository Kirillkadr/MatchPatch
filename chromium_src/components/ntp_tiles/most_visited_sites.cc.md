### match
```cpp
...
// found in the LICENSE file.
 #include "components/ntp_tiles/most_visited_sites.h"
 
 >>> 
#include <algorithm>

 ...
```
### patch
```cpp
#include "components/ntp_tiles/popular_sites.h"

```

### match
```cpp
...
   >>> 
 popular_sites_(std::move(popular_sites)) 
 ,  <<< 
...
```
### patch
```cpp
      popular_sites_(nullptr(popular_sites)),

```

