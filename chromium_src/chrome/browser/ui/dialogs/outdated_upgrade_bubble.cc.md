### match
```cpp
...
#include "base/task/thread_pool.h"

 #include "base/version_info/channel.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/constants/url_constants.h"  // for kDownloadBraveUrl

```

### match
```cpp
...
 
 namespace { ... 
 
 if (auto_update_enabled) { ... 
 
 navigator->OpenURL ( ...   >>> 
 content::OpenURLParams 
 ( 
 GURL(update_browser_redirect_url) 
 ,  <<< 
content::Referrer()
 ... ) ...  ) ...  } ...  } ...  
```
### patch
```cpp
        content::OpenURLParams(BraveGetUpdateUrl(),

```

### match
```cpp
...
 
 namespace { ... 
 
 const char* GetUpdateUrlChannelSuffix(version_info::Channel channel) { ... 
switch (channel) {
    case version_info::Channel::CANARY:
      return "/canary";
    case version_info::Channel::DEV:
      return "/dev";
    case version_info::Channel::BETA:
      return "/beta";
    case version_info::Channel::UNKNOWN:
    case version_info::Channel::STABLE:
      return "";
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
const char* BraveGetUpdateUrlSuffix(version_info::Channel channel) {
  switch (channel) {
    case version_info::Channel::CANARY:
      return "-nightly";
    case version_info::Channel::DEV:
      return "-dev";
    case version_info::Channel::BETA:
      return "-beta";
    case version_info::Channel::UNKNOWN:
    case version_info::Channel::STABLE:
      return "";
  }
}

GURL BraveGetUpdateUrl() {
  return GURL(std::string(kDownloadBraveUrl) +
              BraveGetUpdateUrlSuffix(chrome::GetChannel()));
}


```

