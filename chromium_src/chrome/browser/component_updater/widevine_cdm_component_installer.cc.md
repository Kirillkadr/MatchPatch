### match
```
...
#include "base/values.h"

 #include "base/version.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/browser/widevine/widevine_utils.h"

```

### match
```
...
 namespace component_updater { ...   >>> 
 void 
 RegisterWidevineCdmComponent(ComponentUpdateService* cus) 
 {  <<< ... 
auto installer = base::MakeRefCounted<ComponentInstaller>(
      std::make_unique<WidevineCdmComponentInstallerPolicy>());
 ... } ...  } ...  
```
### patch
```
void RegisterWidevineCdmComponent_ChromiumImpl(ComponentUpdateService* cus) {

```

### match
```
...
 namespace component_updater { ... 
 void RegisterWidevineCdmComponent_ChromiumImpl(ComponentUpdateService* cus) { ... 
installer->Register(cus, base::OnceClosure());
 } 
 >>> 
 ... } ...  
```
### patch
```
void RegisterWidevineCdmComponent(ComponentUpdateService* cus,
                                  base::OnceClosure callback) {
  DCHECK_CURRENTLY_ON(content::BrowserThread::UI);
  if (!IsWidevineEnabled()) {
    return;
  }
  auto installer = base::MakeRefCounted<component_updater::ComponentInstaller>(
      std::make_unique<WidevineCdmComponentInstallerPolicy>());
  installer->Register(cus, std::move(callback));
}



```

