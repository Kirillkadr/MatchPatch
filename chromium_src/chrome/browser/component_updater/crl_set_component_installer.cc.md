### match
```
...
// found in the LICENSE file.
 #include "chrome/browser/component_updater/crl_set_component_installer.h"
 
 >>> 
#include <memory>

 ... 
```
### patch
```
#include "brave/components/brave_component_updater/browser/brave_on_demand_updater.h"

```

### match
```
...
#include "content/public/browser/browser_thread.h"

 #include "content/public/browser/network_service_instance.h"
 
 >>> 
#include "net/cert/crl_set.h"

 ... 
```
### patch
```
#include "chrome/browser/browser_process.h"

```

### match
```
...
#include "net/ssl/ssl_config_service.h"

 #include "services/cert_verifier/public/mojom/cert_verifier_service_factory.mojom.h"
 
 >>> 
namespace component_updater { ...
}
 ... 
```
### patch
```
#if !BUILDFLAG(IS_ANDROID)
#include "chrome/browser/component_updater/component_updater_utils.h"
#include "extensions/common/constants.h"
#endif


```

### match
```
...
 namespace component_updater { ...   >>> 
 void 
 RegisterCRLSetComponent(ComponentUpdateService* cus) 
 {  <<< ... 
auto installer = base::MakeRefCounted<ComponentInstaller>(
      std::make_unique<CRLSetPolicy>());
 ... } ...  } ...  
```
### patch
```
void RegisterCRLSetComponent_ChromiumImpl(ComponentUpdateService* cus) {

```

### match
```
...
 namespace component_updater { ... 
 void RegisterCRLSetComponent_ChromiumImpl(ComponentUpdateService* cus) { ... 
installer->Register(cus, base::OnceClosure());
 } 
 >>> 
 ... } ...  
```
### patch
```
void OnCRLSetRegistered() {
// https://github.com/brave/browser-android-tabs/issues/857
#if !BUILDFLAG(IS_ANDROID)
  brave_component_updater::BraveOnDemandUpdater::GetInstance()->EnsureInstalled(
      crl_set_extension_id);
#endif
}

void RegisterCRLSetComponent(ComponentUpdateService* cus) {
  auto installer = base::MakeRefCounted<component_updater::ComponentInstaller>(
      std::make_unique<CRLSetPolicy>());
  installer->Register(g_browser_process->component_updater(),
                      base::BindOnce(&OnCRLSetRegistered));
}


```

