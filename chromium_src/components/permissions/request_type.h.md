### match
```cpp
...
 
 # ifndef ... 
#define COMPONENTS_PERMISSIONS_REQUEST_TYPE_H_

 #include <optional>
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include <optional>

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace gfx { ... 
 } 
 >>> 
 ... 
```
### patch
```cpp
namespace permissions {
RequestType ContentSettingsTypeToRequestType(
    ContentSettingsType content_settings_type);

std::optional<ContentSettingsType> RequestTypeToContentSettingsType(
    RequestType request_type);

bool IsRequestablePermissionType(ContentSettingsType content_settings_type);

}  // namespace permissions

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ...   >>> 
 kStorageAccess 
 ,  <<< 
kVrSession
 ... } ...  
```
### patch
```cpp
  kStorageAccess, kWidevine, kBraveEthereum, kBraveSolana, kBraveOpenAIChat, \
      kBraveGoogleSignInPermission, kBraveCardano,                           \
      kBraveMinValue = kWidevine, kBraveMaxValue = kBraveCardano,

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
#if BUILDFLAG(IS_ANDROID)
// On Android, icons are represented with an IDR_ identifier.
using IconId = int;
#else
// On desktop, we use a vector icon.
typedef const gfx::VectorIcon& IconId;
#endif  >>> 
 bool IsRequestablePermissionType(ContentSettingsType content_settings_type);  <<< 
std::optional<RequestType> ContentSettingsTypeToRequestTypeIfExists(
    ContentSettingsType content_settings_type);
 ... } ...  
```
### patch
```cpp
bool IsRequestablePermissionType_ChromiumImpl(ContentSettingsType content_settings_type);

```
