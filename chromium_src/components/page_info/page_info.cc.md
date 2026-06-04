### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/page_info/page_info.h"

 ...
```
### patch
```cpp
#include "components/page_info/page_info.h"

```

### match
```cpp
...
ContentSettingsType kTwoPatternPermissions[] = {
    ContentSettingsType::STORAGE_ACCESS,
}; 
 >>> 
 ...
```
### patch
```cpp
#define PageInfo PageInfo_ChromiumImpl

```

### match
```cpp
...
 bool PageInfo::ShouldShowPermission ( ... 
 const PageInfo::PermissionInfo& info 
 ) 
 const 
 { 
 >>> 
// For the Clapper experiment Chrome should display NOTIFICATIONS
 ... } ...  
```
### patch
```cpp
    if (!delegate_->BraveShouldShowPermission(info.type)) \
    return false;

```

### match
```cpp
...
 
 #if BUILDFLAG(IS_CHROMEOS ) ... 
 
 bool PageInfo::ShouldSyncCookiesForCurrentUrl() { ... 
return delegate_->ShouldSyncCookiesForUrl(site_url_);
 } 
 >>> 
 ... 
```
### patch
```cpp
#undef PageInfo

```

