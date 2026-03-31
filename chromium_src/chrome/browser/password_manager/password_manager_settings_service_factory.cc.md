### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/password_manager/password_manager_settings_service_factory.h"

 ... 
```
### patch
```cpp
#if BUILDFLAG(IS_ANDROID)
#include "chrome/browser/password_manager/android/password_manager_android_util.h"
#endif

```

### match
```cpp
...
#include "chrome/browser/password_manager/password_manager_settings_service_factory.h"

 #include "base/trace_event/trace_event.h"
 
 >>> 
#include "chrome/browser/profiles/profile.h"

 ... 
```
### patch
```cpp
#include "build/build_config.h"

```

### match
```cpp
...
 
 std::unique_ptr<password_manager::PasswordManagerSettingsService>
PasswordManagerSettingsServiceFactory::CreateService(Profile* profile) const { ... 
 if ( ...   >>> 
 password_manager_android_util::PasswordManagerUtilBridge 
 > 
 () 
 ) 
 ) 
 {  <<< 
return std::make_unique<PasswordManagerSettingsServiceAndroidImpl>(
        profile->GetPrefs(), SyncServiceFactory::GetForProfile(profile));
 ... } ...  } ...  
```
### patch
```cpp
              password_manager_android_util::PasswordManagerUtilBridge>())|| true) {
    return std::make_unique<
        password_manager::PasswordManagerSettingsServiceImpl>(
        profile->GetPrefs());
  } else if (false /* NOLINT(readability/braces) */) {

```

