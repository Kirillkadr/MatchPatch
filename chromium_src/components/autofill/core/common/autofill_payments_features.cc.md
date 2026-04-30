### match
```cpp
...
// found in the LICENSE file.
 #include "components/autofill/core/common/autofill_payments_features.h"
 >>> 
 ...
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
bool ShouldShowImprovedUserConsentForCreditCardSave() {
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_APPLE) || BUILDFLAG(IS_LINUX)
  // The new user consent UI is fully launched on MacOS, Windows and Linux.
  return true;
#else
  // Chrome OS does not have the new UI.
  return false;
#endif
} 
 >>> 
 ...
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kAutofillEnableAmountExtraction, base::FEATURE_DISABLED_BY_DEFAULT},
    {kAutofillEnableBuyNowPayLater, base::FEATURE_DISABLED_BY_DEFAULT},
    {kAutofillEnableCardBenefitsForAmericanExpress,
     base::FEATURE_DISABLED_BY_DEFAULT},
    {kAutofillEnableCardBenefitsForBmo, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

