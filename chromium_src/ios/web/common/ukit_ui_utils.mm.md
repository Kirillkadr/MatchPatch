### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#import "ios/web/common/uikit_ui_util.h"

 ... 
```
### patch
```cpp
#include "base/apple/foundation_util.h"

```

### match
```cpp
...
#import <UIKit/UIKit.h>

 #import "base/apple/foundation_util.h"
 
 >>> 
UIWindow* GetAnyKeyWindow() {
  for (UIScene* scene in UIApplication.sharedApplication.connectedScenes) {
    UIWindowScene* windowScene =
        base::apple::ObjCCastStrict<UIWindowScene>(scene);
    // Find a key window if it exists.
    for (UIWindow* window in windowScene.windows) {
      if (window.isKeyWindow) {
        return window;
      }
    }
  }

  return nil;
}

UIInterfaceOrientation GetInterfaceOrientation() {
  return GetAnyKeyWindow().windowScene.interfaceOrientation;
}
 ... 
```
### patch
```cpp
// Replaces the strict cast to a standard cast since its possible for Brave to
// have a non-window scene thanks to the CarPlay support

```

### match
```cpp
...
 
 UIWindow* GetAnyKeyWindow() { ...   >>> 
 base::apple::ObjCCastStrict<UIWindowScene>(scene) 
 ;  <<< 
// Find a key window if it exists.
 ... } ...  
```
### patch
```cpp
        base::apple::ObjCCast<UIWindowScene>(scene);

```

