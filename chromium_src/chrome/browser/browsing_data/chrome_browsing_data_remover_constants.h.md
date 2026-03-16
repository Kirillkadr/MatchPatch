### match
```
...
 # ifndef ... 
#include <stdint.h>

 #include "build/build_config.h"
 
 >>> 
#include "chrome/common/buildflags.h"

 ... 
```
### patch
```
#include "brave/components/ai_chat/core/common/buildflags/buildflags.h"

```

### match
```
...
 # ifndef ... 
 namespace 
 chrome_browsing_data_remover 
 { 
 >>> 
// This is an extension of content::BrowsingDataRemover::RemoveDataMask which
 ... } ...  
```
### patch
```
constexpr DataType GetBraveDataTypeValue(const int index) {
  return DataType(1) << (63 - index);
#if BUILDFLAG(ENABLE_AI_CHAT)
inline constexpr DataType DATA_TYPE_BRAVE_LEO_HISTORY =
    GetBraveDataTypeValue(0);
#endif


```

