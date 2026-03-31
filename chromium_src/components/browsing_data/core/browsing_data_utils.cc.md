### match
```cpp
...
// found in the LICENSE file.
 #include "components/browsing_data/core/browsing_data_utils.h"
 
 >>> 
#include <optional>

 ... 
```
### patch
```cpp
#include <optional>
#include <string_view>
#include "base/containers/fixed_flat_map.h"
#include "base/containers/map_util.h"
#include "brave/components/ai_chat/core/common/buildflags/buildflags.h"

```

### match
```cpp
...
>>>
 bool 
 GetDeletionPreferenceFromDataType 
 (  <<< 
BrowsingDataType data_type
 ... ) ...  
```
### patch
```cpp
bool GetDeletionPreferenceFromDataType_ChromiumImpl(

```

### match
```cpp
...
 
 namespace browsing_data { ... 
 
 bool GetDeletionPreferenceFromDataType_ChromiumImpl(
BrowsingDataType data_type,
    ClearBrowsingDataTab clear_browsing_data_tab,
    std::string* out_pref) { ... 
 case 
 BrowsingDataType::TABS 
 : 
 >>> 
return false;
 ... } ...  } ...  
```
### patch
```cpp
      #if BUILDFLAG(ENABLE_AI_CHAT)
        case BrowsingDataType::BRAVE_AI_CHAT
      #endif

```

### match
```cpp
...
 
 namespace browsing_data { ... 
 
 bool GetDeletionPreferenceFromDataType_ChromiumImpl(
BrowsingDataType data_type,
    ClearBrowsingDataTab clear_browsing_data_tab,
    std::string* out_pref) { ... 
 case 
 BrowsingDataType::TABS 
 : 
 >>> 
*out_pref = prefs::kCloseTabs;
 ... } ...  } ...  
```
### patch
```cpp
    #if BUILDFLAG(ENABLE_AI_CHAT)
        case BrowsingDataType::BRAVE_AI_CHAT
    #endif

```

### match
```cpp
...
>>>
 std::optional<BrowsingDataType> 
 GetDataTypeFromDeletionPreference 
 (  <<< 
const std::string& pref_name
 ... ) ...  
```
### patch
```cpp
std::optional<BrowsingDataType> GetDataTypeFromDeletionPreference_ChromiumImpl(

```

### match
```cpp
...
 
 namespace browsing_data { ... 
 
 bool IsHttpsCookieSourceScheme(net::CookieSourceScheme cookie_source_scheme) { ... 
switch (cookie_source_scheme) {
    case net::CookieSourceScheme::kSecure:
      return true;
    case net::CookieSourceScheme::kNonSecure:
      return false;
    case net::CookieSourceScheme::kUnset:
      // Older cookies don't have a source scheme. Associate them with https
      // since the majority of pageloads are https.
      return true;
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool GetDeletionPreferenceFromDataType(
    BrowsingDataType data_type,
    ClearBrowsingDataTab clear_browsing_data_tab,
    std::string* out_pref) {
#if BUILDFLAG(ENABLE_AI_CHAT)
  if (clear_browsing_data_tab == ClearBrowsingDataTab::ADVANCED &&
      data_type == BrowsingDataType::BRAVE_AI_CHAT) {
    *out_pref = prefs::kDeleteBraveLeoHistory;
    return true;
  }
#endif

  return GetDeletionPreferenceFromDataType_ChromiumImpl(
      data_type, clear_browsing_data_tab, out_pref);
}

std::optional<BrowsingDataType> GetDataTypeFromDeletionPreference(
    const std::string& pref_name) {
#if BUILDFLAG(ENABLE_AI_CHAT)
  static constexpr auto kPreferenceToDataType =
      base::MakeFixedFlatMap<std::string_view, BrowsingDataType>({
          {prefs::kDeleteBraveLeoHistory, BrowsingDataType::BRAVE_AI_CHAT},
          {prefs::kDeleteBraveLeoHistoryOnExit,
           BrowsingDataType::BRAVE_AI_CHAT},
      });

  if (const auto* data_type =
          base::FindOrNull(kPreferenceToDataType, pref_name)) {
    return *data_type;
  }
#endif
  return GetDataTypeFromDeletionPreference_ChromiumImpl(pref_name);
}


```

