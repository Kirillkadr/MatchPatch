### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/page_content_annotations/core/page_content_annotations_features.h"

 ... 
```
### patch
```cpp
#include "components/page_content_annotations/core/page_content_annotations_features.h"

```

### match
```cpp
...
 
 namespace page_content_annotations::features { ...   >>> 
 bool 
 ShouldEnablePageContentAnnotations() 
 {  <<< 
// Allow for the validation experiment or remote page metadata to enable the
 ... } ...  } ...  
```
### patch
```cpp
bool ShouldEnablePageContentAnnotations_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace page_content_annotations::features { ... 
 
 bool IsSupportedCountryForFeature(const std::string& country_code,
                                  const base::Feature& feature,
                                  const std::string& default_value) { ... 
return IsSupportedCountry(country_code, value);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool ShouldEnablePageContentAnnotations() {
  return false;
}

```

