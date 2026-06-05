### match
```cpp
...
#include "components/sessions/content/content_serialized_navigation_driver.h"

>>> 
 #include <utility>
 
<<< 
#include "base/memory/singleton.h"

 ... 
```
### patch
```cpp
#include <utility>
#include <string>

#include "base/containers/fixed_flat_set.h"
#include "components/sessions/core/serialized_navigation_entry.h"
#include "content/public/common/url_constants.h"

```

### match
```cpp
...
 
 namespace sessions { ... 
 std::string

>>> 
 ContentSerializedNavigationDriver::GetSanitizedPageStateForPickle 
 ( 
<<< 
const SerializedNavigationEntry* navigation
 ... ) ...  } ...  
```
### patch
```cpp
ContentSerializedNavigationDriver::GetSanitizedPageStateForPickle_ChromiumImpl(

```

### match
```cpp
...
 
 namespace sessions { ... 
 
 const ContentSerializedNavigationDriver::ExtendedInfoHandlerMap&
ContentSerializedNavigationDriver::GetAllExtendedInfoHandlers() const { ... 
return extended_info_handler_map_;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
namespace {
// Extension can override below three chrome urls.
// https://source.chromium.org/chromium/chromium/src/+/main:chrome/common/extensions/api/chrome_url_overrides.idl
constexpr auto kAllowedChromeUrlsOverridingHostList =
    base::MakeFixedFlatSet<std::string_view>(
        {"newtab", "history", "bookmarks"});

}  // namespace

std::string ContentSerializedNavigationDriver::GetSanitizedPageStateForPickle(
    const sessions::SerializedNavigationEntry* navigation) const {
  const auto& virtual_url = navigation->virtual_url();
  if (virtual_url.SchemeIs(content::kChromeUIScheme)) {
    // If empty string is returned, chrome url overriding is ignored.
    if (kAllowedChromeUrlsOverridingHostList.contains(virtual_url.host())) {
      // chrome url can be re-written when it's restored during the tab but
      // re-written url is ignored when encoded page state is empty.
      // In ContentSerializedNavigationBuilder::ToNavigationEntry(), re-written
      // url created by NavigationEntry's ctor is ignored by creating new page
      // state with navigation's virtual_url. Sanitize all but make url info
      // persisted. Use original_request_url as it's used when NavigationEntry
      // is created.
      return blink::PageState::CreateFromURL(navigation->original_request_url())
          .ToEncodedData();
    }
    return std::string();
  }

  return GetSanitizedPageStateForPickle_ChromiumImpl(navigation);
}

```

