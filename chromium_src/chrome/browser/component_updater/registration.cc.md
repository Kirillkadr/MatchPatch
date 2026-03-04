### match
```
...
#include "base/path_service.h"

 #include "base/task/thread_pool.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/browser/brave_browser_process.h"
#include "brave/components/brave_user_agent/browser/brave_user_agent_component_installer.h"
#include "brave/components/brave_wallet/common/buildflags/buildflags.h"
#include "brave/components/local_ai/browser/local_models_updater.h"
#include "brave/components/p3a/component_installer.h"
#include "brave/components/p3a/p3a_service.h"
#include "brave/components/psst/buildflags/buildflags.h"

```

### match
```
...
#include "chrome/browser/component_updater/chrome_origin_trials_component_installer.h"

 #include "chrome/browser/component_updater/commerce_heuristics_component_installer.h"
 
 >>> 
#include "chrome/browser/component_updater/crl_set_component_installer.h"

 ... 
```
### patch
```
#include "chrome/browser/component_updater/component_updater_utils.h"

```

### match
```
...
// Copyright 2020 The Chromium Authors
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

#include "chrome/browser/component_updater/registration.h"

#include "base/feature_list.h"
#include "base/files/file_path.h"
#include "base/files/file_util.h"
#include "base/functional/bind.h"
#include "base/functional/callback.h"
#include "base/metrics/histogram_functions.h"
#include "base/path_service.h"
#include "base/task/thread_pool.h"
#include "brave/browser/brave_browser_process.h"
#include "brave/components/brave_user_agent/browser/brave_user_agent_component_installer.h"
#include "brave/components/brave_wallet/common/buildflags/buildflags.h"
#include "brave/components/local_ai/browser/local_models_updater.h"
#include "brave/components/p3a/component_installer.h"
#include "brave/components/p3a/p3a_service.h"
#include "brave/components/psst/buildflags/buildflags.h"
#include "build/build_config.h"
#include "chrome/browser/browser_process.h"
#include "chrome/browser/buildflags.h"
#include "chrome/browser/component_updater/app_provisioning_component_installer.h"
#include "chrome/browser/component_updater/captcha_provider_component_installer.h"
#include "chrome/browser/component_updater/chrome_origin_trials_component_installer.h"
#include "chrome/browser/component_updater/commerce_heuristics_component_installer.h"
#include "chrome/browser/component_updater/component_updater_utils.h"
#include "chrome/browser/component_updater/crl_set_component_installer.h"
#include "chrome/browser/component_updater/crowd_deny_component_installer.h"
#include "chrome/browser/component_updater/first_party_sets_component_installer.h"
#include "chrome/browser/component_updater/hyphenation_component_installer.h"
#include "chrome/browser/component_updater/mei_preload_component_installer.h"
#include "chrome/browser/component_updater/pki_metadata_component_installer.h"
#include "chrome/browser/component_updater/privacy_sandbox_attestations_component_installer.h"
#include "chrome/browser/component_updater/ssl_error_assistant_component_installer.h"
#include "chrome/browser/component_updater/subresource_filter_component_installer.h"
#include "chrome/browser/component_updater/trust_token_key_commitments_component_installer.h"
#include "chrome/browser/history_embeddings/history_embeddings_utils.h"
#include "chrome/common/buildflags.h"
#include "chrome/common/chrome_paths.h"
#include "components/autofill/core/common/autofill_payments_features.h"
#include "components/component_updater/component_updater_service.h"
#include "components/component_updater/installer_policies/history_search_strings_component_installer.h"
#include "components/component_updater/installer_policies/on_device_head_suggest_component_installer.h"
#include "components/component_updater/installer_policies/optimization_hints_component_installer.h"
#include "components/component_updater/installer_policies/plus_address_blocklist_component_installer.h"
#include "components/component_updater/installer_policies/safety_tips_component_installer.h"
#include "components/on_device_translation/buildflags/buildflags.h"
#include "components/safe_browsing/core/common/features.h"
#include "device/vr/buildflags/buildflags.h"
#include "third_party/widevine/cdm/buildflags.h"
#include "ui/accessibility/accessibility_features.h"

#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC)
#include "chrome/browser/component_updater/recovery_improved_component_installer.h"
#endif  // BUILDFLAG(IS_WIN) || BUILDFLAG(IS_MAC)


 #if 
 BUILDFLAG(IS_ANDROID) 
 >>> 
 ... 
```
### patch
```
#include "chrome/browser/component_updater/zxcvbn_data_component_installer.h"

```

### match
```
...
#include "chrome/browser/component_updater/file_type_policies_component_installer.h"

 #endif 
 >>> 
 ... 
```
### patch
```
#if BUILDFLAG(ENABLE_PSST)
#include "brave/components/psst/browser/core/psst_component_installer.h"
#endif

#if BUILDFLAG(ENABLE_BRAVE_WALLET)
#include "brave/components/brave_wallet/browser/wallet_data_files_installer.h"
#endif  // BUILDFLAG(ENABLE_BRAVE_WALLET)


```

### match
```
...
 namespace component_updater { ...   >>> 
 void 
 RegisterComponentsForUpdate() 
 {  <<< ... 
auto* const cus = g_browser_process->component_updater();
 ... } ...  } ...  
```
### patch
```
void RegisterComponentsForUpdate_ChromiumImpl() {

```

### match
```
...
 namespace component_updater { ... 
 void RegisterComponentsForUpdate_ChromiumImpl() { ... 
if (base::PathService::Get(chrome::DIR_USER_DATA, &path)) {
    if (!history_embeddings::IsHistoryEmbeddingsFeatureEnabled()) {
      DeleteHistorySearchStringsComponent(path);
    }
    base::ThreadPool::PostTask(
        FROM_HERE, {base::TaskPriority::BEST_EFFORT, base::MayBlock()},
        base::BindOnce(&DeleteOldComponents, path));
  }
 } 
 >>> 
 ... } ...  
```
### patch
```
void RegisterComponentsForUpdate() {
  RegisterComponentsForUpdate_ChromiumImpl();
  ComponentUpdateService* cus = g_browser_process->component_updater();
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
  brave_wallet::WalletDataFilesInstaller::GetInstance()
      .MaybeRegisterWalletDataFilesComponent(cus,
                                             g_browser_process->local_state());
#endif  // BUILDFLAG(ENABLE_BRAVE_WALLET)
#if BUILDFLAG(ENABLE_PSST)
  psst::RegisterPsstComponent(cus);
#endif
  p3a::MaybeToggleP3AComponent(cus, g_brave_browser_process->p3a_service());
#if BUILDFLAG(IS_ANDROID)
  // Currently behind !BUILDFLAG(IS_ANDROID) in upstream.
  RegisterZxcvbnDataComponent(cus);
#endif  // BUILDFLAG(IS_ANDROID)
  brave_user_agent::RegisterBraveUserAgentComponent(cus);
  local_ai::ManageLocalModelsComponentRegistration(cus);
}


```

