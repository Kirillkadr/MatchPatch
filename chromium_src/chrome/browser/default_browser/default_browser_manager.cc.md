### match
```
...
#include "base/task/task_traits.h"

 #include "base/task/thread_pool.h"
 
 >>> 
#include "chrome/browser/browser_process.h"

 ... 
```
### patch
```
#include "brave/browser/brave_shell_integration.h"

```

### match
```
...
 
 namespace { ... 
 
 class ShellDelegateImpl : public DefaultBrowserManager::ShellDelegate { ... 
 
 void StartCheckIsDefault(
      shell_integration::DefaultWebClientWorkerCallback callback) override { ...   >>> 
 base::MakeRefCounted<shell_integration::DefaultBrowserWorker>() 
 ;  <<<  ...} ...  } ...  } ...  
```
### patch
```
        base::MakeRefCounted<shell_integration::BraveDefaultBrowserWorker>();

```

