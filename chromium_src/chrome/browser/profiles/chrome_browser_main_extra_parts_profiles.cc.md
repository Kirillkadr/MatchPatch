### match
```cpp
...
#include <utility>

 #include "base/feature_list.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/browser_context_keyed_service_factories.h"

```

### match
```cpp
...
>>>
 void 
 AddProfilesExtraParts(ChromeBrowserMainParts* main_parts) 
 {  <<< 
main_parts->AddParts(std::make_unique<ChromeBrowserMainExtraPartsProfiles>());
 ... } ...  
```
### patch
```cpp
void AddProfilesExtraParts(ChromeBrowserMainParts_ChromiumImpl* main_parts) {

```

### match
```cpp
...
 
 void ChromeBrowserMainExtraPartsProfiles::
    EnsureBrowserContextKeyedServiceFactoriesBuilt() { ... 
if (base::FeatureList::IsEnabled(syncer::kWebApkBackupAndRestoreBackend)) {
    webapk::WebApkSyncServiceFactory::GetInstance();
  }
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
  brave::EnsureBrowserContextKeyedServiceFactoriesBuilt();

```

