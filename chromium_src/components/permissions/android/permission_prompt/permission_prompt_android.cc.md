### match
```cpp
...
#include <memory>

 #include <vector>
 
 >>> 
#include "base/android/jni_array.h"

 ... 
```
### patch
```cpp
#include "base/feature_list.h"
#include "components/permissions/features.h"

```

### match
```cpp
...
 
 namespace permissions { ... 
 using base::android::ConvertUTF16ToJavaString; 
 >>> 
PermissionPromptAndroid::PermissionPromptAndroid(
    content::WebContents* web_contents,
    Delegate* delegate)
    : web_contents_(web_contents), delegate_(delegate) {
  DCHECK(web_contents);
  std::transform(delegate_->Requests().begin(), delegate_->Requests().end(),
                 std::back_inserter(requests_),
                 [](const std::unique_ptr<PermissionRequest>& request_ptr) {
                   return request_ptr->GetWeakPtr();
                 });
}
 ... } ...  
```
### patch
```cpp
#define PermissionPromptAndroid PermissionPromptAndroid_ChromiumImpl

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 bool PermissionPromptAndroid::ShouldShowLocationPrecisionSelector() const { ... 
return delegate_->ShouldShowLocationPrecisionSelector();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
#undef PermissionPromptAndroid
int PermissionPromptAndroid::GetIconId() const {
  const auto& requests = delegate()->Requests();
  if (requests.size() == 1) {
    if (requests[0]->request_type() == RequestType::kStorageAccess) {
      return permissions::GetIconId(requests[0]->request_type());
    }
  }
  return PermissionPromptAndroid_ChromiumImpl::GetIconId();
}
bool PermissionPromptAndroid::ShouldUseRequestingOriginFavicon() const {
  return false;
}

```

