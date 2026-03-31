### match
```cpp
...
#include "chrome/browser/browser_process.h"

 #include "chrome/browser/profiles/profile.h"
 
 >>> 
#include "components/permissions/prediction_service/prediction_service.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/profiles/profile_selections.h"

```

### match
```cpp
...
 
 std::unique_ptr<KeyedService>
PredictionServiceFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const { ... 
return std::make_unique<permissions::PredictionService>(
      network::SharedURLLoaderFactory::Create(std::move(url_loader_factory)));
 } 
 >>> 
 ... 
```
### patch
```cpp
// static
permissions::PredictionService* PredictionServiceFactory::GetForProfile(
    Profile* profile) {
  return nullptr;
}

// static
PredictionServiceFactory* PredictionServiceFactory::GetInstance() {
  static base::NoDestructor<PredictionServiceFactory> instance;
  return instance.get();
}

void PredictionServiceFactory::set_prediction_service_for_testing(
    permissions::PredictionService* service) {
  CHECK_IS_TEST();
  prediction_service_for_testing_ = service;
}

PredictionServiceFactory::PredictionServiceFactory()
    : ProfileKeyedServiceFactory("PredictionService",
                                 ProfileSelections::BuildNoProfilesSelected()) {
}

PredictionServiceFactory::~PredictionServiceFactory() = default;

std::unique_ptr<KeyedService>
PredictionServiceFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const {
  return nullptr;
}
```

