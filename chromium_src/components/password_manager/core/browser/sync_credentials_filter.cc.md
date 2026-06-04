### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/password_manager/core/browser/sync_credentials_filter.h"

 ... 
```
### patch
```cpp
#include "components/password_manager/core/browser/sync_credentials_filter.h"

```

### match
```cpp
...
 
 namespace password_manager { ...   >>> 
 bool 
 SyncCredentialsFilter::ShouldSave(const PasswordForm& form) const 
 {  <<< 
if (client_->IsOffTheRecord()) {
    return false;
  }
 ... } ...  } ...  
```
### patch
```cpp
bool SyncCredentialsFilter::ShouldSave_ChromiumImpl(const PasswordForm& form) const {

```

### match
```cpp
...
 
 namespace password_manager { ... 
 
 bool SyncCredentialsFilter::IsSyncAccountEmail(
    const std::string& username) const { ... 
return sync_util::IsSyncAccountEmail(username, client_->GetIdentityManager(),
                                       signin::ConsentLevel::kSync);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool SyncCredentialsFilter::ShouldSave(const PasswordForm& form) const {
  bool should_save = ShouldSave_ChromiumImpl(form);
  if (!should_save && sync_util::IsGaiaCredentialPage(form.signon_realm)) {
    return true;
  }
  return should_save;
}

```

