### match
```cpp
...
#include "content/public/browser/web_contents.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
constexpr char kHatsShouldShowSurveyReasonAndroidHistogram[] =
    "Feedback.HappinessTrackingSurvey.ShouldShowSurveyReasonAndroid";
 ... 
```
### patch
```cpp
#define HatsServiceAndroid HatsServiceAndroid_ChromiumImpl


```

### match
```cpp
...
 
 bool HatsServiceAndroid::HasPendingTasksForTesting() { ... 
return !pending_tasks_.empty();
 } 
 >>> 
 ... 
```
### patch
```cpp

#undef HatsServiceAndroid

HatsServiceAndroid::HatsServiceAndroid(Profile* profile)
    : HatsServiceAndroid_ChromiumImpl(profile) {}

HatsServiceAndroid::~HatsServiceAndroid() = default;

bool HatsServiceAndroid::CanShowSurvey(const std::string& trigger) const {
  return false;
}
```

