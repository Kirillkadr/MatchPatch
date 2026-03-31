### match
```cpp
...
// found in the LICENSE file.
 #include "components/component_updater/component_installer.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp

#include "base/check.h"
#include "base/logging.h"
#include "build/build_config.h"


```

### match
```cpp
...
#include <utility>

 #include <vector>
 
 >>> 
#include "base/files/file_enumerator.h"

 ... 
```
### patch
```cpp
#include "base/containers/fixed_flat_set.h"

```

### match
```cpp
...
 
 namespace component_updater { ...   >>> 
 void 
 ComponentInstaller::Register 
 ( 
 ComponentUpdateService* cus 
 ,  <<< 
base::OnceClosure callback
 ... ) ...  } ...  
```
### patch
```cpp
void ComponentInstaller::Register_ChromiumImpl(ComponentUpdateService* cus,

```

### match
```cpp
...
>>>
 Register 
 ( 
 base::BindOnce 
 ( 
 &ComponentUpdateService::RegisterComponent 
 ,  <<< 
base::Unretained(cus)
 ... ) ...  ) ...  
```
### patch
```cpp
  Register_ChromiumImpl(base::BindOnce(&ComponentUpdateService::RegisterComponent,

```

### match
```cpp
...
 
 namespace component_updater { ...   >>> 
 void 
 ComponentInstaller::Register 
 (  <<< 
RegisterCallback register_callback
 ... ) ...  } ...  
```
### patch
```cpp
void ComponentInstaller::Register_ChromiumImpl(

```

### match
```cpp
...
 
 namespace component_updater { ... 
 
 void ComponentInstaller::ComponentReady(base::DictValue manifest) { ... 
installer_policy_->ComponentReady(current_version_, current_install_dir_,
                                    std::move(manifest));
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool ComponentInstallerPolicy::IsBraveComponent() const {
  return false;
}
void ComponentInstaller::Register(ComponentUpdateService* cus,
                                  base::OnceClosure callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  DCHECK(cus);
  Register(base::BindOnce(&ComponentUpdateService::RegisterComponent,
                          base::Unretained(cus)),
           std::move(callback));
}

void ComponentInstaller::Register(
    RegisterCallback register_callback,
    base::OnceClosure callback,
    const base::Version& registered_version,
    const base::Version& max_previous_product_version) {
  static constexpr auto kDisallowedComponents =
      base::MakeFixedFlatSet<std::string_view>({
          "bklopemakmnopmghhmccadeonafabnal",  // Legacy TLS Deprecation Config
          "cmahhnpholdijhjokonmfdjbfmklppij",  // Federated Learning of Cohorts
          "eeigpngbgcognadeebkilcpcaedhellh",  // Autofill States Data
          "gcmjkmgdlgnkkcocmoeiminaijmmjnii",  // Subresource Filter Rules
          "imefjhfbkmcmebodilednhmaccmincoa",  // Client Side Phishing Detection
          "llkgjffcdpffmhiakmfcdcblohccpfmo",  // Origin Trials
          "gonpemdgkjcecdgbnaabipppbmgfggbe",  // First Party Sets
          "dhlpobdgcjafebgbbhjdnapejmpkgiie",  // Desktop Sharing Hub
          "ldfkbgjbencjpgjfleiooeldhjdapggh",  // Probabilistic Reveal Tokens
          "hajigopbbjhghbfimgkfmpenfkclmohk",  // Amount Extraction Heuristic
                                               // Regexes
          "bjbcblmdcnggnibecjikpoljcgkbgphl",  // WASM TTS Engine
          "ninodabcejpeglfjbkhdplaoglpcbffj",  // Actor Safety Lists
#if BUILDFLAG(IS_ANDROID)
          "lmelglejhemejginpboagddgdfbepgmp",  // Optimization Hints
          "obedbbhbpmojnkanicioggnmelmoomoc"   // OnDeviceHeadSuggest
#endif
      });
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  if (installer_policy_) {
    std::vector<uint8_t> hash;
    installer_policy_->GetHash(&hash);
    const std::string id = update_client::GetCrxIdFromPublicKeyHash(hash);
    if (kDisallowedComponents.contains(id)) {
      VLOG(1) << "Skipping registration of Brave-unsupported component " << id
              << ".";
      return;
    }
  }
  Register_ChromiumImpl(std::move(register_callback), std::move(callback),
                        registered_version, max_previous_product_version);
}

bool ComponentInstaller::IsBraveComponent() const {
  return installer_policy_->IsBraveComponent();
}

```

