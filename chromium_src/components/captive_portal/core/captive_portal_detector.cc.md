### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/captive_portal/core/captive_portal_detector.h"

 ... 
```
### patch
```cpp
#include "components/captive_portal/core/captive_portal_detector.h"

```

### match
```cpp
...
 
 namespace { ... 
 "http://connectivitycheck.gstatic.com/generate_204" 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp

constexpr char kBraveDefaultURL[] = "http://detectportal.brave-http-only.com/";


```

### match
```cpp
...
 
 namespace captive_portal { ...   >>> 
 const 
 std::string_view 
 CaptivePortalDetector::GetDefaultUrl() 
 {  <<< 
return base::FeatureList::IsEnabled(features::kCaptivePortalUpdatedOrigin)
             ? kDefaultURL
             : kLegacyURL;
 ... } ...  } ...  
```
### patch
```cpp
const std::string_view CaptivePortalDetector::GetDefaultUrl_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace captive_portal { ... 
 
 bool CaptivePortalDetector::FetchingURL() const { ... 
return simple_loader_ != nullptr;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// static
const std::string_view CaptivePortalDetector::GetDefaultUrl_ChromiumImpl() {
  return kBraveDefaultURL;
}

```

