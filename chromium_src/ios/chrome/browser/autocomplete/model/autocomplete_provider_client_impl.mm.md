### match
```
...
#import "ios/components/webui/web_ui_url_constants.h"

 #import "services/network/public/cpp/shared_url_loader_factory.h"
 
 >>> 
AutocompleteProviderClientImpl::AutocompleteProviderClientImpl(
    ProfileIOS* profile)
    : profile_(profile),
      url_consent_helper_(
          unified_consent::UrlKeyedDataCollectionConsentHelper::
              NewAnonymizedDataCollectionConsentHelper(profile_->GetPrefs())),
      personalized_url_consent_helper_(
          unified_consent::UrlKeyedDataCollectionConsentHelper::
              NewPersonalizedDataCollectionConsentHelper(
                  SyncServiceFactory::GetForProfile(profile_))),
      omnibox_triggered_feature_service_(
          std::make_unique<OmniboxTriggeredFeatureService>()),
      tab_matcher_(profile_) {
  pedal_provider_ = std::make_unique<OmniboxPedalProvider>(
      *this, GetPedalImplementations(IsOffTheRecord(), false));
}
 ... 
```
### patch
```
void AutocompleteProviderClientImpl::OpenLeo(const std::u16string& query) {}

bool AutocompleteProviderClientImpl::IsLeoProviderEnabled() {
  return false;
}


```

