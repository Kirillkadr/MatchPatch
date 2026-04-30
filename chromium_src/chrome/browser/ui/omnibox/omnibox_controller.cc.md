### match
```cpp
...
#include "base/time/time.h"

 #include "base/trace_event/trace_event.h"
 
 >>> 
#include "chrome/browser/preloading/preloading_features.h"

 ... 
```
### patch
```cpp
#include "brave/components/omnibox/browser/brave_omnibox_prefs.h"

```

### match
```cpp
...
#include "components/omnibox/browser/page_classification_functions.h"

 #include "components/omnibox/browser/prewarm_trigger.h"
 
 >>> 
#include "components/search_engines/template_url_starter_pack_data.h"

 ... 
```
### patch
```cpp
#include "components/prefs/pref_service.h"

```

### match
```cpp
...
#include "components/search_engines/template_url_starter_pack_data.h"

 #include "ui/gfx/geometry/rect.h"
 
 >>> 
OmniboxController::OmniboxController(
    std::unique_ptr<OmniboxClient> client,
    std::optional<base::TimeDelta> autocomplete_stop_timer_duration)
    : client_(std::move(client)),
      edit_model_(std::make_unique<OmniboxEditModel>(
          /*omnibox_controller=*/this)),
      popup_state_manager_(std::make_unique<OmniboxPopupStateManager>()) {
  AutocompleteControllerConfig autocomplete_controller_config{
      .provider_types = AutocompleteClassifier::DefaultOmniboxProviders()};
  if (omnibox::IsWebUIOmniboxPopupEnabled()) {
    autocomplete_controller_config.show_iph_matches = false;
  }
  if (autocomplete_stop_timer_duration.has_value()) {
    autocomplete_controller_config.stop_timer_duration =
        autocomplete_stop_timer_duration.value();
  }
  autocomplete_controller_ = std::make_unique<AutocompleteController>(
      client_->CreateAutocompleteProviderClient(),
      autocomplete_controller_config);

  // Register the `AutocompleteController` with `AutocompleteControllerEmitter`.
  if (auto* emitter = client_->GetAutocompleteControllerEmitter()) {
    autocomplete_controller_->AddObserver(emitter);
  }
}
 ... 
```
### patch
```cpp
namespace {

bool IsAutocompleteEnabled(const PrefService* prefs) {
  return prefs->GetBoolean(omnibox::kAutocompleteEnabled);
}

}  // namespace


```

### match
```cpp
...
>>>
 void 
 OmniboxController::StartAutocomplete 
 (  <<< 
const AutocompleteInput& input
 ... ) ...  
```
### patch
```cpp
void OmniboxController::StartAutocomplete_ChromiumImpl(

```

### match
```cpp
...
 
 void OmniboxController::StartAutocomplete_ChromiumImpl(
const AutocompleteInput& input) const { ... 
autocomplete_controller_->Start(input);
 } 
 >>> 
 ... 
```
### patch
```cpp
void OmniboxController::StartAutocomplete(
    const AutocompleteInput& input) const {
  if (!IsAutocompleteEnabled(client_->GetPrefs())) {
    ClearPopupKeywordMode();
    return;
  }

  StartAutocomplete_ChromiumImpl(input);
}

void OmniboxController::StartZeroSuggestPrefetch() {
  // Disables zero suggest prefetch by doing nothing in here.
}


```

