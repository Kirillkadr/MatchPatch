### match
```cpp
...
#include "base/strings/utf_string_conversions.h"

 #include "base/trace_event/trace_event.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/common/resource_bundle_helper.h"

```

### match
```cpp
...
>>>
 std::string 
 LoadLocalState 
 (  <<< 
ChromeFeatureListCreator* chrome_feature_list_creator
 ... ) ...  
```
### patch
```cpp
std::string LoadLocalState_ChromiumImpl(

```

### match
```cpp
...
 
 std::string LoadLocalState_ChromiumImpl(
ChromeFeatureListCreator* chrome_feature_list_creator,
    bool is_running_tests) { ... 
return InitResourceBundleAndDetermineLocale(
      chrome_feature_list_creator->local_state(), is_running_tests);
 } 
 >>> 
 ... 
```
### patch
```cpp

std::string LoadLocalState(
    ChromeFeatureListCreator* chrome_feature_list_creator,
    bool is_running_tests) {
  std::string ret = LoadLocalState_ChromiumImpl(chrome_feature_list_creator,
                                                is_running_tests);
  brave::InitializeResourceBundle();
  return ret;
}
```

