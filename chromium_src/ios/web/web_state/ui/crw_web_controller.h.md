### match
```cpp
...
 
 # ifndef ... 
#import "ios/web/web_state/ui/crw_web_view_navigation_proxy.h"

 #import "ios/web/web_state/web_view_pass_key.h"
 
 >>> 
namespace web {

enum class BackForwardNavigationType;
enum class NavigationInitiationType;
enum Permission : NSUInteger;
enum PermissionState : NSUInteger;
enum class WKNavigationState;

}
 ... 
```
### patch
```cpp
@class CRWWebView;

```

### match
```cpp
...
 
 # ifndef ... 
property(strong, nonatomic, readonly) id<CRWWebViewProxy> webViewProxy;
 // The web view navigation proxy associated with this controller. 
 >>> 
@
 ... 
```
### patch
```cpp
@property(weak, nonatomic, readonly) id<CRWWebViewNavigationProxy>
    webViewNavigationProxy_ChromiumImpl;                               

```

### match
```cpp
...
 webViewNavigationProxy 
 ; 
 >>> 
 ... 
```
### patch
```cpp
  @property(weak, nonatomic, readonly) CRWWebView* webView;

```

