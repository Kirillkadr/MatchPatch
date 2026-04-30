### match
```cpp
...
// found in the LICENSE file.
 #include "content/test/content_test_suite.h"
 
 >>> 
#include "base/base_paths.h"

 ... 
```
### patch
```cpp
#include <algorithm>
#include "base/sanitizer_buildflags.h"
#include "build/build_config.h"

```

### match
```cpp
...
#include "ui/gl/init/gl_factory.h"

 #include "ui/gl/test/gl_surface_test_support.h"
 
 >>> 
#if BUILDFLAG(IS_WIN)
#include "ui/display/win/dpi.h"
#endif
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_WIN) && !BUILDFLAG(IS_ANDROID) && !BUILDFLAG(USING_SANITIZER)
#include <array>
#include <string_view>

#include "base/feature_list.h"
#endif

```

### match
```cpp
...
#include "base/test/mock_chrome_application_mac.h"

 #endif 
 >>> 
 ... 
```
### patch
```cpp
#if !BUILDFLAG(IS_WIN) && !BUILDFLAG(IS_ANDROID) && !BUILDFLAG(USING_SANITIZER)
namespace {
constexpr std::array<std::string_view, 1> kFieldTrialExceptions = {
    "FledgeEnforceKAnonymity",
};
}
#endif




```

### match
```cpp
...
 
 namespace content { ... 
 
 ContentTestSuite::ContentTestSuite(int argc, char** argv)
    : ContentTestSuiteBase(argc, argv) { ... 
 
 #if !BUILDFLAG(IS_WIN ) ... 
CHECK(feature_list->GetEnabledFieldTrialByFeatureName(feature));
 disabled_field_trial.push_back(feature); 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp

#if !BUILDFLAG(IS_WIN) && !BUILDFLAG(IS_ANDROID) && !BUILDFLAG(USING_SANITIZER)
    CHECK(feature_list->GetEnabledFieldTrialByFeatureName(FEATURE) ||    
      std::ranges::contains(kFieldTrialExceptions, FEATURE));
    disabled_field_trial.push_back(feature);
#endif


```

