### match
```cpp
...
// found in the LICENSE file.
 #include "components/component_updater/component_updater_service.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp
#include "base/notreached.h"
#include "components/component_updater/component_installer.h"
#include "components/component_updater/component_updater_service_internal.h"

```

### match
```cpp
...
 
 namespace component_updater { ... 
 
 void RegisterComponentUpdateServicePrefs(PrefRegistrySimple* registry) { ... 
registry->RegisterBooleanPref(prefs::kComponentUpdatesEnabled,
                                kComponentUpdatesEnabledByDefault);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void CrxUpdateService::EnsureInstalled(const std::string& id,
                                       Callback callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);

  std::optional<ComponentRegistration> component_registration =
      GetComponent(id);

  // If the component is not registered, return.
  if (!component_registration) {
    if (callback) {
      base::SequencedTaskRunner::GetCurrentDefault()->PostTask(
          FROM_HERE, base::BindOnce(std::move(callback),
                                    update_client::Error::INVALID_ARGUMENT));
    }
    return;
  }

  // If the component is already installed, return.
  if (component_registration->version != base::Version(kNullVersion)) {
    if (callback) {
      base::SequencedTaskRunner::GetCurrentDefault()->PostTask(
          FROM_HERE,
          base::BindOnce(std::move(callback), update_client::Error::NONE));
    }
    return;
  }

  auto crx_data_callback = base::BindOnce(&CrxUpdateService::GetCrxComponents,
                                          base::Unretained(this));
  auto update_complete_callback = base::BindOnce(
      &CrxUpdateService::OnUpdateComplete, base::Unretained(this),
      std::move(callback), base::TimeTicks::Now());

  update_client_->Install(id, std::move(crx_data_callback), {},
                          std::move(update_complete_callback));
}

void CrxUpdateService::OnDemandUpdate(const std::vector<std::string>& ids,
                                      Priority priority,
                                      Callback callback) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);

  for (const auto& id : ids) {
    if (!GetComponent(id)) {
      if (callback) {
        base::SequencedTaskRunner::GetCurrentDefault()->PostTask(
            FROM_HERE, base::BindOnce(std::move(callback),
                                      update_client::Error::INVALID_ARGUMENT));
      }
      return;
    }
  }

  auto crx_data_callback = base::BindOnce(&CrxUpdateService::GetCrxComponents,
                                          base::Unretained(this));
  auto update_complete_callback = base::BindOnce(
      &CrxUpdateService::OnUpdateComplete, base::Unretained(this),
      std::move(callback), base::TimeTicks::Now());

  update_client_->Update(ids, std::move(crx_data_callback), {},
                         priority == Priority::FOREGROUND,
                         std::move(update_complete_callback));
}

void OnDemandUpdater::EnsureInstalled(const std::string& id,
                                      Callback callback) {
  NOTREACHED();
}

void OnDemandUpdater::OnDemandUpdate(const std::vector<std::string>& ids,
                                     Priority priority,
                                     Callback callback) {
  NOTREACHED();
}

```

