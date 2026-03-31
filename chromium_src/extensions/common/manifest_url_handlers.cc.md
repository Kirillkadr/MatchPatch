### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "extensions/common/manifest_url_handlers.h"

 ... 
```
### patch
```cpp
#include "extensions/common/manifest_url_handlers.h"

```

### match
```cpp
...
#include "extensions/common/manifest_url_handlers.h"

 #include "extensions/common/manifest_url_handlers.h"
 
 >>> 
#include <memory>

 ... 
```
### patch
```cpp
#include "extensions/common/constants.h"

```

### match
```cpp
...
 
 namespace extensions { ...   >>> 
 GURL 
 ManifestURL::GetHomepageURL(const Extension* extension) 
 {  <<< 
const GURL& homepage_url = Get(extension, keys::kHomepageURL);
 ... } ...  } ...  
```
### patch
```cpp
GURL ManifestURL::GetHomepageURL_Unused(const Extension* extension) {

```

### match
```cpp
...
 
 namespace extensions { ... 
 
 GURL ManifestURL::GetHomepageURL_Unused(const Extension* extension) { ... 
const GURL& homepage_url = Get(extension, keys::kHomepageURL);  >>> 
 return homepage_url.is_valid() ? homepage_url : GetWebStoreURL(extension);  <<<  ...} ...  } ...  
```
### patch
```cpp
  return homepage_url.is_valid() ? homepage_url : GetWebStoreURL_ChromiumImpl(extension);

```

### match
```cpp
...
 
 namespace extensions { ...   >>> 
 GURL 
 ManifestURL::GetWebStoreURL(const Extension* extension) 
 {  <<< 
bool use_webstore_url = UpdatesFromGallery(extension) &&
                          !SharedModuleInfo::IsSharedModule(extension);
 ... } ...  } ...  
```
### patch
```cpp
GURL ManifestURL::GetWebStoreURL_ChromiumImpl(const Extension* extension) {

```

### match
```cpp
...
 
 namespace extensions { ... 
 
 base::span<const char* const> AboutPageHandler::Keys() const { ... 
return kKeys;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// We need to provide our own version of GetHomepageURL() as well to make sure
// that we get our own version of GetWebStoreURL() called when invoked via
// GetHomepageURL(). Otherwise the old version will still be called since the
// renaming of GetWebStoreURL() above does also modify the call point.
const GURL ManifestURL::GetHomepageURL(const Extension* extension) {
  const GURL& homepage_url = Get(extension, keys::kHomepageURL);
  if (homepage_url.is_valid()) {
    return homepage_url;
  }
  return GetWebStoreURL(extension);
}

// static
const GURL ManifestURL::GetWebStoreURL(const Extension* extension) {
  if (extensions_mv2::IsKnownBraveHostedExtension(extension->id())) {
    return GURL::EmptyGURL();
  }
  return GetWebStoreURL_ChromiumImpl(extension);
}

```

