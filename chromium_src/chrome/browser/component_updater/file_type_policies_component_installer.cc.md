### match
```
...
#include "base/task/thread_pool.h"

 #include "base/version.h"
 
 >>> 
#include "components/component_updater/component_updater_paths.h"

 ... 
```
### patch
```
#include "brave/components/brave_component_updater/browser/brave_on_demand_updater.h"
#include "chrome/browser/component_updater/component_updater_utils.h"

```

### match
```
...
#include "chrome/browser/component_updater/component_updater_utils.h"

 #include "components/component_updater/component_updater_paths.h"
 
 >>> 
#include "components/safe_browsing/content/common/file_type_policies.h"

 ... 
```
### patch
```
#include "components/component_updater/component_updater_service.h"

```

### match
```
...
 namespace component_updater { ...   >>> 
 void 
 RegisterFileTypePoliciesComponent(ComponentUpdateService* cus) 
 {  <<< ... 
VLOG(1) << "Registering File Type Policies component.";
 ... } ...  } ...  
```
### patch
```
void RegisterFileTypePoliciesComponent_ChromiumImpl(ComponentUpdateService* cus) {

```

### match
```
...
 namespace component_updater { ... 
 void RegisterFileTypePoliciesComponent_ChromiumImpl(ComponentUpdateService* cus) { ... 
installer->Register(cus, base::OnceClosure());
 } 
 >>> 
 ... } ...  
```
### patch
```
constexpr char kFileTypePoliciesComponentId[] =
    "khaoiebndkojlmppeemjhbpbandiljpe";

void OnFileTypePoliciesRegistered() {
  brave_component_updater::BraveOnDemandUpdater::GetInstance()->EnsureInstalled(
      kFileTypePoliciesComponentId);
}

void RegisterFileTypePoliciesComponent(ComponentUpdateService* cus) {
  auto installer = base::MakeRefCounted<ComponentInstaller>(
      std::make_unique<FileTypePoliciesComponentInstallerPolicy>());
  installer->Register(cus, base::BindOnce(&OnFileTypePoliciesRegistered));
}


```

