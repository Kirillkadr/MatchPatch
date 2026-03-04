### match
```
...
 # ifndef ... 
#include "chrome/browser/startup_data.h"
  >>> 
 #include "brave/common/brave_content_client.h"
  <<< ... 
#include "chrome/common/chrome_content_client.h"

 ... 
```
### patch
```

```

### match
```
...
 # ifndef ... 
std::unique_ptr<tracing::TracingSamplerProfiler> tracing_sampler_profiler_;  >>> 
 BraveContentClient chrome_content_client_;  <<< ... 
memory_system::MemorySystem memory_system_;
 ... 
```
### patch
```
  ChromeContentClient chrome_content_client_;

```

