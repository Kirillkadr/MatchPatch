### match
```
...
#include "url/gurl.h"

 #include "url/url_constants.h"
 
 >>> 
#if BUILDFLAG(SAFE_BROWSING_AVAILABLE)
#include "chrome/browser/safe_browsing/user_interaction_observer.h"
#include "components/safe_browsing/core/common/safe_browsing_prefs.h"
#endif
 ... 
```
### patch
```
#include "extensions/buildflags/buildflags.h"

#if BUILDFLAG(ENABLE_EXTENSIONS)
#include "extensions/common/extension_urls.h"
#endif

```

### match
```
...
 namespace actor { ... 
mojom::ActionResultCode BlockReasonToResultCode(MayActOnUrlBlockReason reason,
                                                bool for_navigation) {
  using mojom::ActionResultCode;

  const ActionResultCode generic_block_code =
      for_navigation ? ActionResultCode::kTriggeredNavigationBlocked
                     : ActionResultCode::kUrlBlocked;

  auto maybe_granular = [generic_block_code](
                            mojom::ActionResultCode specific_code) {
    return base::FeatureList::IsEnabled(kGlicGranularBlockingActionResultCodes)
               ? specific_code
               : generic_block_code;
  };

  switch (reason) {
    case MayActOnUrlBlockReason::kAllowed:
      return ActionResultCode::kOk;
    case MayActOnUrlBlockReason::kExternalProtocol: {
      if (base::FeatureList::IsEnabled(kGlicExternalProtocolActionResultCode)) {
        return ActionResultCode::kExternalProtocolNavigationBlocked;
      }
      return generic_block_code;
    }
    case MayActOnUrlBlockReason::kLookalikeDomain:
    case MayActOnUrlBlockReason::kBlockedByStaticList:
      return maybe_granular(ActionResultCode::kActionsBlockedForSiteRisk);
    case MayActOnUrlBlockReason::kSafeBrowsing:
      return maybe_granular(
          ActionResultCode::kActionsBlockedSafeBrowsingDisabled);
    case MayActOnUrlBlockReason::kEnterprisePolicy:
      return maybe_granular(
          ActionResultCode::kActionsBlockedByEnterprisePolicy);
    case MayActOnUrlBlockReason::kWrongScheme:
      return maybe_granular(ActionResultCode::kActionsBlockedForScheme);
    case MayActOnUrlBlockReason::kTabIsErrorDocument:
      return maybe_granular(ActionResultCode::kActionsBlockedOnErrorPage);
    case MayActOnUrlBlockReason::kIpAddress:
    case MayActOnUrlBlockReason::kOptimizationGuideBlock:
    case MayActOnUrlBlockReason::kUrlNotInAllowlist:
      return generic_block_code;
  }
}
 } 
 // namespace actor 
 >>> 
 ... 
```
### patch
```

namespace {

bool IsChromeWebStoreURL(const GURL& url) {
#if BUILDFLAG(ENABLE_EXTENSIONS)
  return (url.GetHost() == extension_urls::GetWebstoreLaunchURL().GetHost()) ||
         (url.GetHost() == extension_urls::GetNewWebstoreLaunchURL().GetHost());
#else
  return false;
#endif
}

}  // namespace

// Add Brave-specific restrictions
#define BRAVE_MAY_ACT_ON_URL_INTERNAL                       \
  if (IsChromeWebStoreURL(url)) {                           \
    decision_wrapper->Reject(                               \
        "Extension store URL",                              \
        actor::MayActOnUrlBlockReason::kUrlNotInAllowlist); \
    return;                                                 \
  }
```