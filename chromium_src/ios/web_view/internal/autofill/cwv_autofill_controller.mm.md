### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#import <algorithm>

 ... 
```
### patch
```cpp
#pragma clang diagnostic push
#pragma clang diagnostic ignored "-Wnullability-completeness"
#include <memory>

#include "base/functional/callback_forward.h"
#include "components/autofill/ios/browser/autofill_client_ios.h"
#include "ios/web/public/web_state.h"
#include "ios/web_view/internal/autofill/cwv_autofill_client_ios_bridge.h"
#include "ios/web_view/internal/autofill/cwv_autofill_controller_internal.h"
#include "ios/web_view/internal/autofill/web_view_autofill_client_ios.h"

```

### match
```cpp
...
- (BOOL)hasValidState {
  return _webState && _passwordManagerClient;
}
 @ 
 end 
 >>> 
 ... 
```
### patch
```cpp
@implementation CWVAutofillController (Internal)
- (instancetype)
         initWithWebState:(web::WebState*)webState
     createAutofillClient:(CreateAutofillClientCallback)createAutofillClient
            autofillAgent:(AutofillAgent*)autofillAgent
          passwordManager:(std::unique_ptr<password_manager::PasswordManager>)
                              passwordManager
    passwordManagerClient:
        (std::unique_ptr<ios_web_view::WebViewPasswordManagerClient>)
            passwordManagerClient
       passwordController:(SharedPasswordController*)passwordController {
  self = [self initWithWebState:webState
          autofillClientForTest:createAutofillClient.Run(webState, nil)
                  autofillAgent:autofillAgent
                passwordManager:std::move(passwordManager)
          passwordManagerClient:std::move(passwordManagerClient)
             passwordController:passwordController];
  // Overwrite the autofill client with one that has a valid bridge arg
  _autofillClient = createAutofillClient.Run(webState, self);
  return self;
}

@end

#pragma clang diagnostic pop

```

