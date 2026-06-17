### match
```cpp
...
 #include <string>
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/memory/scoped_refptr.h"
#include "components/wallet/core/browser/network/wallet_http_client.h"

```

### match
```cpp
...
 #include "services/network/public/mojom/url_response_head.mojom.h"
 
 >>> 
 ... 
```
### patch
```cpp
namespace signin {
class IdentityManager;
}
namespace network {
class SharedURLLoaderFactory;
}

namespace wallet {

class WalletHttpClientImpl : public WalletHttpClient {
 public:
  WalletHttpClientImpl(
      signin::IdentityManager* identity_manager,
      scoped_refptr<network::SharedURLLoaderFactory> url_loader_factory);
  ~WalletHttpClientImpl() override;

  WalletHttpClientImpl(const WalletHttpClientImpl&) = delete;
  WalletHttpClientImpl& operator=(const WalletHttpClientImpl&) = delete;

  // WalletHttpClient:
  void SavePass(const WalletablePass& pass, SavePassCallback callback) override;
};

}  // namespace wallet

```

