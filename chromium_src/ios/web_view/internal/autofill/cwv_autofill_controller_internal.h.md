### match
```cpp
...
 NS_ASSUME_NONNULL_END 
 >>> 
 ... 
```
### patch
```cpp
using CreateAutofillClientCallback =
    base::RepeatingCallback<std::unique_ptr<autofill::WebViewAutofillClientIOS>(
        web::WebState*,
        id<CWVAutofillClientIOSBridge, AutofillDriverIOSBridge>)>;
// Expose a way to create an CWVAutofillController with a explicit
// WebViewAutofillClientIOS so we can avoid it making one with WebView factories
@interface CWVAutofillController (Internal)
- (instancetype)initWithWebState:(web::WebState*)webState
            createAutofillClient:
                (CreateAutofillClientCallback)createAutofillClientCallback
                   autofillAgent:(AutofillAgent*)autofillAgent
                 passwordManager:
                     (std::unique_ptr<password_manager::PasswordManager>)
                         passwordManager
           passwordManagerClient:
               (std::unique_ptr<ios_web_view::WebViewPasswordManagerClient>)
                   passwordManagerClient
              passwordController:(SharedPasswordController*)passwordController;
@end

```

