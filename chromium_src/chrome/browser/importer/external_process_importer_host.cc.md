### match
```
...
#include <memory>

 #include "base/functional/bind.h"
 
 >>> 
#include "chrome/browser/bookmarks/bookmark_model_factory.h"

 ... 
```
### patch
```
#include "brave/browser/importer/brave_external_process_importer_client.h"
#include "brave/browser/importer/brave_in_process_importer_bridge.h"

```

### match
```
...
>>>
 InProcessImporterBridge 
 * bridge 
 = 
 new 
 InProcessImporterBridge 
 ( 
 writer_.get() 
 ,  <<< 
weak_ptr_factory_.GetWeakPtr()
 ... ) ...  
```
### patch
```
  BraveInProcessImporterBridge* bridge =
      new BraveInProcessImporterBridge(writer_.get(),

```

### match
```
...
>>>
 client_ 
 = 
 new 
 ExternalProcessImporterClient 
 (  <<< 
weak_ptr_factory_.GetWeakPtr()
 ... ) ...  
```
### patch
```
  client_ = new BraveExternalProcessImporterClient(

```

