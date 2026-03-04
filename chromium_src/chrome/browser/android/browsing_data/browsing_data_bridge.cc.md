### match
```
...
#include "content/public/browser/web_contents.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
// Must come after all headers that specialize FromJniType() / ToJniType().
 ... 
```
### patch
```
#include "brave/components/ai_chat/core/common/buildflags/buildflags.h"

```

### match
```
...
 DEFINE_JNI(BrowsingDataBridge) 
 >>> 
 ... 
```
### patch
```

#if BUILDFLAG(ENABLE_AI_CHAT)
#define BRAVE_CLEAR_BROWSING_DATA                                             \
  remove_mask |= BrowsingDataRemover::DATA_TYPE_DOWNLOADS;                    \
  break;                                                                      \
  case browsing_data::BrowsingDataType::BRAVE_AI_CHAT:                        \
    remove_mask |= chrome_browsing_data_remover::DATA_TYPE_BRAVE_LEO_HISTORY; \
    break;
#else
#define BRAVE_CLEAR_BROWSING_DATA                          \
  remove_mask |= BrowsingDataRemover::DATA_TYPE_DOWNLOADS; \
  break;
#endif

#undef BRAVE_CLEAR_BROWSING_DATA
```

