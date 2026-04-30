### match
```cpp
...
// found in the LICENSE file.
 #include "components/autofill/core/browser/payments/offer_notification_handler.h"
 
 >>> 
#include "components/autofill/core/browser/data_model/payments/autofill_offer_data.h"

 ... 
```
### patch
```cpp
#include "components/autofill/core/browser/data_model/payments/autofill_offer_data.h"
#include "components/autofill/core/browser/payments/autofill_offer_manager.h"

```

### match
```cpp
...
 namespace 
 autofill 
 { 
 >>> 
namespace {

bool IsOfferValid(const AutofillOfferData* offer) {
  if (!offer) {
    return false;
  }

  if (offer->GetMerchantOrigins().empty()) {
    return false;
  }

  if (offer->GetOfferType() == AutofillOfferData::OfferType::UNKNOWN) {
    return false;
  }

  return true;
}

}
 ... } ...  
```
### patch
```cpp
namespace {
// This replicates the functionality that the removed upstream flag
// kAutofillEnableOfferNotificationForPromoCodes used to have.
bool BraveIsOfferValid(const AutofillOfferData* offer) {
  if (!offer) {
    return false;
  }

  if (offer->IsPromoCodeOffer()) {
    return false;
  }

  return true;
}

}  // namespace

```

### match
```cpp
...
 
 namespace autofill { ... 
 
 bool OfferNotificationHandler::ValidOfferExistsForUrl(const GURL& url) { ...   >>> 
 return 
 offer_manager_->IsUrlEligible(url) 
 &&  <<< 
IsOfferValid(offer_manager_->GetOfferForUrl(url))
 ... } ...  } ...  
```
### patch
```cpp
  return offer_manager_->IsUrlEligible(URL) && BraveIsOfferValid(offer_manager_->GetOfferForUrl(URL)) &&

```

