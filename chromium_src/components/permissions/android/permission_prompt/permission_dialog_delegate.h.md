### match
```cpp
...
 
 # ifndef ... 
#define COMPONENTS_PERMISSIONS_ANDROID_PERMISSION_PROMPT_PERMISSION_DIALOG_DELEGATE_H_

 #include <variant>
 
 >>> 
#include "base/android/scoped_java_ref.h"

 ... 
```
### patch
```cpp
// Forward includes to avoid redefine of Create term
#include "base/task/cancelable_task_tracker.h"
#include "components/permissions/permission_util.h"
#include "content/public/browser/web_contents_observer.h"
// Forward includes to avoid redefine of CreateDialog term
#include "components/permissions/android/permission_prompt/permission_dialog_controller.h"

```

### match
```cpp
...
 
 # ifndef ... 
 namespace 
 permissions 
 { 
 >>> 
class PermissionDialogDelegate
 ... } ...  
```
### patch
```cpp
class PermissionPromptAndroid_ChromiumImpl;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
virtual void CreateJavaDelegate(content::WebContents* web_contents,
                                  PermissionDialogDelegate* owner);  >>> 
 virtual void CreateDialog(content::WebContents* web_contents);  <<< 
void GetAndUpdateRequestingOriginFavicon(content::WebContents* web_contents);
 ... } ...  
```
### patch
```cpp
  virtual void BravePreCreateDialog(JNIEnv* env);
  void CreateDialog(content::WebContents* web_contents);

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
void CreateDialog(content::WebContents* web_contents);
 void GetAndUpdateRequestingOriginFavicon(content::WebContents* web_contents); 
 >>> 
void OnRequestingOriginFaviconLoaded(
      const favicon_base::FaviconRawBitmapResult& favicon_result);
 ... } ...  
```
### patch
```cpp
  void ApplyLifetimeToPermissionRequests(
      JNIEnv* env, PermissionPromptAndroid* permission_prompt);
  void ApplyDontAskAgainOption(JNIEnv* env,
                               PermissionPromptAndroid* permission_prompt);

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 
 class PermissionDialogDelegate : public content::WebContentsObserver { ... 
// The interface for creating a modal dialog when the PermissionRequestManager
 // is enabled. 
 >>> 
static std::unique_ptr<PermissionDialogDelegate> Create(
      content::WebContents* web_contents,
      PermissionPromptAndroid* permission_prompt);
 ... } ...  } ...  
```
### patch
```cpp
  static std::unique_ptr<PermissionDialogDelegate> Create(content::WebContents* web_contents,
         PermissionPromptAndroid_ChromiumImpl* permission_prompt);

```

