### match
```cpp
...
#include "components/commerce/core/commerce_feature_list.h"

 #include <string_view>
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 
 namespace commerce { ... 
bool IsNoDiscountMerchant(const GURL& url) {
  auto* pattern_from_component =
      commerce_heuristics::CommerceHeuristicsData::GetInstance()
          .GetNoDiscountMerchantPattern();
  // If pattern from component updater is not available, merchants are
  // considered to have no discounts by default.
  if (!pattern_from_component) {
    return true;
  }
  return RE2::PartialMatch(url.host(), *pattern_from_component);
}
 #endif 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kCommerceAllowOnDemandBookmarkUpdates, base::FEATURE_DISABLED_BY_DEFAULT},
    {kCommerceDeveloper, base::FEATURE_DISABLED_BY_DEFAULT},
    {kCommerceMerchantViewer, base::FEATURE_DISABLED_BY_DEFAULT},
    {kPriceAnnotations, base::FEATURE_DISABLED_BY_DEFAULT},
    {kShoppingList, base::FEATURE_DISABLED_BY_DEFAULT},
    {kShoppingPDPMetrics, base::FEATURE_DISABLED_BY_DEFAULT},
    {kRetailCoupons, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

