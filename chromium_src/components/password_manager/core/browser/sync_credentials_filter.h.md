### match
```cpp
...
 
 # ifndef ... 
#include "components/password_manager/core/browser/credentials_filter.h"

 #include "components/password_manager/core/browser/password_manager_client.h"
 
 >>> 
namespace password_manager {

struct PasswordForm;

// The sync- and GAIA- aware implementation of the filter.
class SyncCredentialsFilter : public CredentialsFilter {
 public:
  // Implements protection of sync credentials. Uses |client| to get the last
  // committed entry URL for a check against GAIA reauth site.
  explicit SyncCredentialsFilter(PasswordManagerClient* client);

  SyncCredentialsFilter(const SyncCredentialsFilter&) = delete;
  SyncCredentialsFilter& operator=(const SyncCredentialsFilter&) = delete;

  ~SyncCredentialsFilter() override;

  // CredentialsFilter
  bool ShouldSave(const PasswordForm& form) const override;
  bool ShouldSaveGaiaPasswordHash(const PasswordForm& form) const override;
  bool ShouldSaveEnterprisePasswordHash(
      const PasswordForm& form) const override;
  bool IsSyncAccountEmail(const std::string& username) const override;

 private:
  const raw_ptr<PasswordManagerClient> client_;
};

}
 ... 
```
### patch
```cpp
#include "components/password_manager/core/browser/credentials_filter.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace password_manager { ... 
 
 class SyncCredentialsFilter : public CredentialsFilter { ... 
~SyncCredentialsFilter() override;
 // CredentialsFilter 
 >>> 
bool ShouldSave(const PasswordForm& form) const override;
 ... } ...  } ...  
```
### patch
```cpp
  bool ShouldSave_ChromiumImpl(const PasswordForm& form) const; 

```

