### match
```
...
#include "services/network/public/mojom/clear_data_filter.mojom.h"

 #include "third_party/perfetto/include/perfetto/tracing/track.h"
 
 >>> 
#if BUILDFLAG(IS_ANDROID)
#include "chrome/browser/android/customtabs/chrome_origin_verifier.h"
#include "chrome/browser/android/oom_intervention/oom_intervention_decider.h"
#include "chrome/browser/android/webapps/webapp_registry.h"
#include "chrome/browser/feed/feed_service_factory.h"
#include "chrome/browser/offline_pages/offline_page_model_factory.h"
#include "chrome/browser/profiles/profile.h"
#include "chrome/browser/ui/android/tab_model/tab_model.h"
#include "chrome/browser/ui/android/tab_model/tab_model_list.h"
#include "components/cdm/browser/media_drm_storage_impl.h"  // nogncheck crbug.com/1125897
#include "components/feed/core/v2/public/feed_service.h"    // nogncheck
#include "components/feed/feed_feature_list.h"
#include "components/installedapp/android/jni_headers/PackageHash_jni.h"
#include "components/offline_pages/core/offline_page_feature.h"
#include "components/offline_pages/core/offline_page_model.h"
#endif
 ... 
```
### patch
```
#define CHROME_BROWSING_DATA_REMOVER_DELEGATE_GET_HISTORY_SUFFIX \
  case TracingDataType::kIPFSCache:                              \
    return "IPFSCache";
#undef CHROME_BROWSING_DATA_REMOVER_DELEGATE_GET_HISTORY_SUFFIX


```

