### match
```
...
#include "base/functional/bind.h"

 #include "base/functional/callback.h"
 
 >>> 
#include "chrome/browser/shell_integration.h"

 ... 
```
### patch
```
#include "brave/browser/brave_shell_integration.h"

```

### match
```
...
 
 namespace default_browser { ... 
 
 void ShellIntegrationDefaultBrowserSetter::Execute(
    DefaultBrowserSetterCompletionCallback on_complete) { ... 
on_complete_callback_ = std::move(on_complete);  >>> 
 worker_ = base::MakeRefCounted<shell_integration::DefaultBrowserWorker>();  <<< 
worker_->StartSetAsDefault(
      base::BindOnce(&ShellIntegrationDefaultBrowserSetter::OnComplete,
                     weak_ptr_factory_.GetWeakPtr()));
 ... } ...  } ...  
```
### patch
```
  worker_ = base::MakeRefCounted<shell_integration::BraveDefaultBrowserWorker>();

```

