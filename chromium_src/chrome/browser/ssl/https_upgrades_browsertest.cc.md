### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp
#define InitWithFeatures(...) \
  InitWithFeaturesAndDisable(net::features::kBraveHttpsByDefault, __VA_ARGS__)

```

### match
```cpp
...
#include "base/test/metrics/histogram_tester.h"

 #include "base/test/simple_test_clock.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "base/test/scoped_feature_list.h"

```

### match
```cpp
...
#include "content/public/test/test_navigation_observer.h"
  >>> 
 #include "content/public/test/url_loader_interceptor.h"
  <<< 
#include "net/dns/mock_host_resolver.h"

 ... 
```
### patch
```cpp
#include "content/public/test/url_loader_interceptor.h"\
#include "net/base/features.h"

```

### match
```cpp
...
 
 IN_PROC_BROWSER_TEST_F(HttpsUpgradesSecureOriginAllowlistBrowserTest,
                       HostNotInAllowlistShowWarning) { ... 
EXPECT_TRUE(chrome_browser_interstitials::IsShowingHttpsFirstModeInterstitial(
      contents));
 } 
 >>> 
 ... 
```
### patch
```cpp
#undef InitWithFeatures

```

