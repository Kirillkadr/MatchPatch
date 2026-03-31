### match
```cpp
...
#include "base/functional/callback_helpers.h"

 #include "base/i18n/rtl.h"
 
 >>> 
#include "base/memory/raw_ptr.h"

 ... 
```
### patch
```cpp
#include "base/memory/ptr_util.h"

```

### match
```cpp
...
#include "base/memory/ptr_util.h"

 #include "base/memory/raw_ptr.h"
 
 >>> 
#include "base/metrics/histogram_functions.h"

 ... 
```
### patch
```cpp
#include "base/memory/ptr_util.h"

```

### match
```cpp
...
#include "base/task/single_thread_task_runner.h"

 #include "base/time/time.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/constants/pref_names.h"

```

### match
```cpp
...
#include "chrome/browser/ui/autofill/payments/credit_card_scanner_controller.h"

 #include "chrome/browser/ui/autofill/payments/payments_view_factory.h"
 
 >>> 
#include "chrome/browser/ui/autofill/popup_controller_common.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/ui/autofill/payments/webauthn_dialog_controller_impl.h"

```

### match
```cpp
...
#include "components/compose/buildflags.h"

 #include "components/feature_engagement/public/feature_constants.h"
 
 >>> 
#include "components/optimization_guide/content/browser/page_content_proto_provider.h"

 ... 
```
### patch
```cpp
#include "components/optimization_guide/core/optimization_guide_features.h"

```

### match
```cpp
...
#include "content/public/browser/storage_partition.h"

 #include "content/public/common/content_features.h"
 
 >>> 
#include "services/network/public/cpp/shared_url_loader_factory.h"

 ... 
```
### patch
```cpp
#include "mojo/public/cpp/bindings/associated_receiver.h"

```

### match
```cpp
...
 
 namespace autofill { ... 
void ChromeAutofillClient::OnActorTaskStateChange(actor::ActorTask& task) {
  const actor::TaskId task_id = task.id();
  const actor::ActorTask::State state = task.GetState();

  if (active_actor_task_ && *active_actor_task_ != task_id) {
    // The update is for an actor that isn't working on the current tab.
    return;
  }

  // The actor task on this tab has finished.
  // TODO(crbug.com/472336281): The state changes leading to the task
  // completion should be issued before the `ActorTask` gets removed.
  if (actor::ActorTask::IsCompletedState(state)) {
    active_actor_task_.reset();
    return;
  }

  const tabs::TabInterface* tab_interface = GetTabInterface();
  if (tab_interface && !task.HasTab(tab_interface->GetHandle())) {
    // The status update is for an actor that isn't interacting with this tab.
    // The value of `is_actor_mode_` shouldn't be updated.
    return;
  }

  // TODO(crbug.com/469428128): Evaluate whether
  // `actor::ActorTask::State::kCreated` state should enable the actor mode.
  active_actor_task_ = task_id;
}
 } 
 // namespace autofill 
 >>> 
 ... 
```
### patch
```cpp
namespace autofill {

namespace {

bool IsPrivateProfile(content::WebContents* web_contents) {
  if (!web_contents) {
    return false;
  }
  auto* profile =
      Profile::FromBrowserContext(web_contents->GetBrowserContext());
  if (!profile) {
    return false;
  }
  return (profile_metrics::GetBrowserProfileType(profile) ==
          profile_metrics::BrowserProfileType::kIncognito) ||
         profile->IsTor();
}

}  // namespace

class BraveChromeAutofillClient : public ChromeAutofillClient {
 public:
  using ChromeAutofillClient::ChromeAutofillClient;

  AutofillOptimizationGuideDecider* GetAutofillOptimizationGuideDecider()
      const override {
    if (optimization_guide::features::IsOptimizationHintsEnabled()) {
      return ChromeAutofillClient::GetAutofillOptimizationGuideDecider();
    }
    return nullptr;
  }

  bool IsAutocompleteEnabled() const override {
    auto enabled = ChromeAutofillClient::IsAutocompleteEnabled();
    if (!IsPrivateProfile(web_contents())) {
      return enabled;
    }
    enabled = enabled && GetPrefs()->GetBoolean(kBraveAutofillPrivateWindows);
    return enabled;
  }

  bool IsAutofillEnabled() const override {
    auto enabled = ChromeAutofillClient::IsAutofillEnabled();
    if (GetProfileType() != profile_metrics::BrowserProfileType::kIncognito &&
        GetProfileType() !=
            profile_metrics::BrowserProfileType::kOtherOffTheRecordProfile) {
      return enabled;
    }
    enabled = enabled && GetPrefs()->GetBoolean(kBraveAutofillPrivateWindows);
    return enabled;
  }
};

}  // namespace autofill

#define WrapUnique WrapUnique(new autofill::BraveChromeAutofillClient(web_contents))); \
  if (0) std::unique_ptr<autofill::ChromeAutofillClient> dummy(
#include <chrome/browser/ui/autofill/chrome_autofill_client.cc>
#undef WrapUnique

namespace autofill {

AutofillOptimizationGuideDecider*
ChromeAutofillClient::GetAutofillOptimizationGuideDecider_Unused() const {
  return nullptr;
}

bool ChromeAutofillClient::IsAutofillEnabled_Unused() const {
  return false;
}

bool ChromeAutofillClient::IsAutocompleteEnabled_Unused() const {
  return false;
}

}  // namespace autofill


```

