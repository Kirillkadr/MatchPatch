[translate_ui_delegate.cc](translate_ui_delegate.cc)### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ... 
```
### patch
```cpp
#include "components/translate/core/browser/translate_ui_delegate.h"

```

### match
```cpp
...
// Copyright 2014 The Chromium Authors
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

#include "components/translate/core/browser/translate_ui_delegate.h"

 #include "components/translate/core/browser/translate_ui_delegate.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "brave/components/translate/core/common/brave_translate_features.h"

```

### match
```cpp
...
 namespace 
 translate 
 { 
 >>> 
 ... } ...  
```
### patch
```cpp
#define TranslateUIDelegate TranslateUIDelegate_ChromiumImpl

```

### match
```cpp
...
 
 namespace translate { ... 
 
 const TranslateDriver* TranslateUIDelegate::GetTranslateDriver() const { ... 
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
#undef TranslateUIDelegate
bool TranslateUIDelegate::ShouldShowAlwaysTranslateShortcut() const {
  if (!IsBraveAutoTranslateEnabled())
    return false;
  return TranslateUIDelegate_ChromiumImpl::ShouldShowAlwaysTranslateShortcut();
}

#if BUILDFLAG(IS_ANDROID) || BUILDFLAG(IS_IOS)
bool TranslateUIDelegate::ShouldAutoAlwaysTranslate() {
  if (!IsBraveAutoTranslateEnabled())
    return false;

  return TranslateUIDelegate_ChromiumImpl::ShouldAutoAlwaysTranslate();
}
#endif  // BUILDFLAG(IS_ANDROID) || BUILDFLAG(IS_IOS)

```

