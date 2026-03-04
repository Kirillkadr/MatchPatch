### match
```
...
#include "base/strings/utf_string_conversions.h"

 #include "base/threading/thread.h"
 
 >>> 
#include "chrome/browser/bookmarks/bookmark_model_factory.h"

 ... 
```
### patch
```
#include "base/uuid.h"
#include "chrome/browser/autofill/personal_data_manager_factory.h"

```

### match
```
...
#include "chrome/browser/webdata_services/web_data_service_factory.h"

 #include "chrome/common/pref_names.h"
 
 >>> 
#include "components/autofill/core/browser/webdata/autofill_webdata_service.h"

 ... 
```
### patch
```
#include "components/autofill/core/browser/data_manager/personal_data_manager.h"

```

### match
```
...
void ProfileWriter::AddAutocompleteFormDataEntries(
    const std::vector<autofill::AutocompleteEntry>& autocomplete_entries) {
  scoped_refptr<autofill::AutofillWebDataService> web_data_service =
      WebDataServiceFactory::GetAutofillWebDataForProfile(
          profile_, ServiceAccessType::EXPLICIT_ACCESS);
  if (web_data_service.get())
    web_data_service->UpdateAutocompleteEntries(autocomplete_entries);
}
 ProfileWriter::~ProfileWriter() = default; 
 >>> 
 ... 
```
### patch
```

void ProfileWriter::AddCreditCard(const std::u16string& name_on_card,
                                  const std::u16string& expiration_month,
                                  const std::u16string& expiration_year,
                                  const std::u16string& decrypted_card_number,
                                  const std::string& origin) {
  autofill::PersonalDataManager* personal_data =
      autofill::PersonalDataManagerFactory::GetForBrowserContext(profile_);

  autofill::CreditCard credit_card = autofill::CreditCard(
      base::Uuid::GenerateRandomV4().AsLowercaseString(), origin);

  if (!name_on_card.empty()) {
    credit_card.SetRawInfo(autofill::CREDIT_CARD_NAME_FULL,
                           name_on_card);
  }

  if (!decrypted_card_number.empty()) {
    credit_card.SetRawInfo(autofill::CREDIT_CARD_NUMBER,
                           decrypted_card_number);
  }

  if (!expiration_month.empty()) {
    credit_card.SetRawInfo(autofill::CREDIT_CARD_EXP_MONTH,
                           expiration_month);
  }

  if (!expiration_year.empty()) {
    credit_card.SetRawInfo(autofill::CREDIT_CARD_EXP_4_DIGIT_YEAR,
                           expiration_year);
  }

  personal_data->payments_data_manager().AddCreditCard(credit_card);
}

#if BUILDFLAG(IS_ANDROID)
namespace first_run {
bool IsChromeFirstRun() {
  return false;
}
}  // namespace first_run
#endif  // BUILDFLAG(IS_ANDROID)
```

