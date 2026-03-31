### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/ntp_tiles/chrome_popular_sites_factory.h"

 ... 
```
### patch
```cpp
#include "brave/components/ntp_tiles/brave_popular_sites_impl.h"

```

### match
```cpp
...
 
 std::unique_ptr<ntp_tiles::PopularSites>
ChromePopularSitesFactory::NewForProfile(Profile* profile) { ...   >>> 
 return 
 std::make_unique<ntp_tiles::PopularSitesImpl> 
 (  <<< 
profile->GetPrefs()
 ... ) ...  } ...  
```
### patch
```cpp
  return std::make_unique<ntp_tiles::BravePopularSitesImpl>(

```

