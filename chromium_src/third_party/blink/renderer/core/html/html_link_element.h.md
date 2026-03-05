### match
```
...
 # ifndef ... 
#include <memory>

 #include <utility>
 
 >>> 
#include "base/task/single_thread_task_runner.h"

 ... 
```
### patch
```
#include "third_party/blink/renderer/core/loader/link_loader_client.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
// From LinkLoaderClient
 bool ShouldLoadLink() override; 
 >>> 
bool IsLinkCreatedByParser() override;
 ... } ...  
```
### patch
```
  bool NotUsed();
  HTMLLinkElement* GetOwner() override;

```

