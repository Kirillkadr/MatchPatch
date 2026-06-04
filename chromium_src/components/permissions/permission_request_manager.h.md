### match
```cpp
...
 
 # ifndef ... 
#include "ui/gfx/geometry/rect.h"

 class GURL 
 ; 
 >>> 
namespace content {
class RenderFrameHost;
}
 ... 
```
### patch
```cpp
class WidevinePermissionAndroidTest;
class SplitViewCommonBrowserTest;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 
 class PermissionRequestManager
    : public content::WebContentsObserver,
      public content::WebContentsUserData<PermissionRequestManager>,
      public PermissionPrompt::Delegate { ... 
 
 const std::vector<std::unique_ptr<PermissionUiSelector>>&
  get_permission_ui_selectors_for_testing() { ... 
return permission_ui_selectors_;
 } 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void AcceptDenyCancel(const std::vector<PermissionRequest*>& accepted_requests,
                   const std::vector<PermissionRequest*>& denied_requests,
                   const std::vector<PermissionRequest*>& cancelled_requests);
  bool ShouldGroupRequests(PermissionRequest* a, PermissionRequest* b) const;
  void OnTabActiveStateChanged(bool active);

 private:
  void UpdateTabIsHiddenWithTabActivationState();
  bool ShouldBeGrouppedInRequests(PermissionRequest* a) const;
  friend class ::WidevinePermissionAndroidTest;
  friend class ::SplitViewCommonBrowserTest;
  bool tab_is_active_for_testing() const {
    return tab_is_active_;
  }

 public:
  std::optional<bool> tab_is_activated_;

```

