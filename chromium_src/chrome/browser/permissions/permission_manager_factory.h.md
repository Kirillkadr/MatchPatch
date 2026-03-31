### match
```cpp
...
 
 # ifndef ... 
#include "base/no_destructor.h"

 #include "chrome/browser/profiles/profile_keyed_service_factory.h"
 
 >>> 
namespace content {
class BrowserContext;
}
 ... 
```
### patch
```cpp
#include "components/keyed_service/content/browser_context_keyed_service_factory.h"

namespace brave_wallet {
class EthereumProviderImplUnitTest;
class SolanaProviderImplUnitTest;
class CardanoProviderImplUnitTest;
class BraveWalletServiceUnitTest;
}  // namespace brave_wallet

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace permissions { ... 
 class PermissionManager 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
class BraveWalletPermissionContextUnitTest;

```

### match
```cpp
...
 
 # ifndef ... 
 
 class PermissionManagerFactory : public ProfileKeyedServiceFactory { ... 
~PermissionManagerFactory() override;
 // BrowserContextKeyedServiceFactory methods: 
 >>> 
std::unique_ptr<KeyedService> BuildServiceInstanceForBrowserContext(
      content::BrowserContext* profile) const override;
 ... } ...  
```
### patch
```cpp
  std::unique_ptr<KeyedService> BuildServiceInstanceForBrowserContext_ChromiumImpl(       
      content::BrowserContext* profile) const;
  friend brave_wallet::EthereumProviderImplUnitTest;
  friend brave_wallet::SolanaProviderImplUnitTest;
  friend brave_wallet::CardanoProviderImplUnitTest;
  friend brave_wallet::BraveWalletServiceUnitTest;
  friend permissions::BraveWalletPermissionContextUnitTest;

```

