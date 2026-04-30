### match
```cpp
...
// found in the LICENSE file.
 #include "components/affiliations/core/browser/affiliation_fetcher_factory_impl.h"
 
 >>> 
#include "components/affiliations/core/browser/hash_affiliation_fetcher.h"

 ... 
```
### patch
```cpp
#include "components/affiliations/core/browser/hash_affiliation_fetcher.h"

```

### match
```cpp
...
#include "components/affiliations/core/browser/hash_affiliation_fetcher.h"

 #include "services/network/public/cpp/shared_url_loader_factory.h"
 
 >>> 
namespace affiliations {

AffiliationFetcherFactoryImpl::AffiliationFetcherFactoryImpl() = default;
AffiliationFetcherFactoryImpl::~AffiliationFetcherFactoryImpl() = default;

std::unique_ptr<AffiliationFetcherInterface>
AffiliationFetcherFactoryImpl::CreateInstance(
    scoped_refptr<network::SharedURLLoaderFactory> url_loader_factory) {
  return HashAffiliationFetcher::IsFetchPossible()
             ? std::make_unique<HashAffiliationFetcher>(
                   std::move(url_loader_factory))
             : nullptr;
}

bool AffiliationFetcherFactoryImpl::CanCreateFetcher() const {
  return HashAffiliationFetcher::IsFetchPossible();
}

}
 ... 
```
### patch
```cpp
namespace {
class BraveHashAffiliationFetcher
    : public affiliations::HashAffiliationFetcher {
 public:
  using HashAffiliationFetcher::HashAffiliationFetcher;

  void StartRequest(
      const std::vector<affiliations::FacetURI>& facet_uris,
      RequestInfo request_info,
      base::OnceCallback<void(FetchResult)> result_callback) override {}
};

}  // namespace

```

