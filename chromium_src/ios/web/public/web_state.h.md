### match
```cpp
...
 
 # ifndef ... 
#include "ui/base/window_open_disposition.h"

 #include "url/gurl.h"
 
 >>> 
class GURL
 ... 
```
### patch
```cpp
#include <set>
#include <string_view>
#include "base/check.h"
#include "ios/components/webui/web_ui_url_constants.h"
#include "third_party/abseil-cpp/absl/container/flat_hash_map.h"
#include "url/gurl.h"

```

### match
```cpp
...
 
 # ifndef ... 
const raw_ptr<WebState> web_state_;
 std::map<std::string, Callback> callbacks_; 
 >>> 
 ... 
```
### patch
```cpp

 public:
  template <typename Interface>
  void AddUntrustedInterface(
      const GURL& url,
      base::RepeatingCallback<void(mojo::PendingReceiver<Interface>)>
          callback) {
    DCHECK(!url.is_empty() && url.is_valid() &&
           url.SchemeIs(kChromeUIUntrustedScheme));
    untrusted_callbacks_[url.host()].insert(Interface::Name_);

    AddInterface(
        Interface::Name_,
        base::BindRepeating(&WrapCallback<Interface>, std::move(callback)));
  }

  void RemoveUntrustedInterface(const GURL& origin,
                                std::string_view interface_name);

  bool IsAllowedForOrigin(const GURL& origin,
                          std::string_view interface_name);

 private:
  absl::flat_hash_map<std::string, std::set<std::string, std::less<>>>       
      untrusted_callbacks_;

```

