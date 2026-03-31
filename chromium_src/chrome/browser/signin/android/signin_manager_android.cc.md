### match
```cpp
...
// Must come after all headers that specialize FromJniType() / ToJniType().
 #include "chrome/browser/signin/services/android/jni_headers/SigninManagerImpl_jni.h"
 
 >>> 
using base::android::JavaRef;
 ... 
```
### patch
```cpp
#include "brave/build/android/jni_headers/BraveSigninManager_jni.h"
#include "chrome/android/chrome_jni_headers/SigninManagerImpl_jni.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 bool ShouldLoadPolicyForUser(const std::string& username) { ... 
return signin::AccountManagedStatusFinder::MayBeEnterpriseUserBasedOnEmail(
      username);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// For preventing "unused Java_SigninManager_create method" compile error.
class UnusedClass {
 private:
  void test() {
    Java_SigninManagerImpl_create(nullptr, 0ll, nullptr, nullptr, nullptr);
    Java_SigninManagerImpl_destroy(nullptr, 0ll);
  }
};


```

### match
```cpp
...
>>>
 java_signin_manager_ 
 = 
 Java_SigninManagerImpl_create 
 (  <<< 
base::android::AttachCurrentThread()
 ... ) ...  
```
### patch
```cpp
  java_signin_manager_ = Java_BraveSigninManager_create(

```

### match
```cpp
...
>>>
 Java_SigninManagerImpl_destroy 
 ( 
 base::android::AttachCurrentThread() 
 ,  <<<  ...) ...  
```
### patch
```cpp
  Java_BraveSigninManager_destroy(base::android::AttachCurrentThread(),

```

