### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ...
```
### patch
```cpp
#include "components/translate/core/browser/translate_language_list.h"

```

### match
```cpp
...
// Copyright 2013 The Chromium Authors
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

#include "components/translate/core/browser/translate_language_list.h"

 #include "components/translate/core/browser/translate_language_list.h"
 
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
const char TranslateLanguageList::kTargetLanguagesKey[] = "tl";
>>>
...
```
### patch
```cpp
#define TranslateLanguageList TranslateLanguageList_ChromiumImpl

```

### match
```cpp
...
 
 namespace translate { ... 
 >>>  } ...
```
### patch
```cpp
#undef TranslateLanguageList
void TranslateLanguageList::SetResourceRequestsAllowed(bool allowed) {
  if (!ShouldUpdateLanguagesList()) {
    allowed = false;
  }
  TranslateLanguageList_ChromiumImpl::SetResourceRequestsAllowed(allowed);
}

```
