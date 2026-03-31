### match
```cpp
...
// found in the LICENSE file.
 #include "components/download/public/common/download_task_runner.h"
 
 >>> 
#include "base/lazy_instance.h"

 ... 
```
### patch
```cpp
#include "base/check_is_test.h"

```

### match
```cpp
...
 
 namespace download { ... 
 
 scoped_refptr<base::SequencedTaskRunner> GetDownloadDBTaskRunnerForTesting() { ... 
return g_db_task_runner.Get();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// IOTaskRunner is set on global variable. Once a task runner is set, we can't
// change global IOTaskRunner. But this makes unit tests flaky because tasks
// are posted to wrong runner - typically, tasks could be posted to the runner
// created by previous test, not to what we want to post the tasks.
void ClearIOTaskRunnerForTesting() {
  CHECK_IS_TEST();
  g_io_task_runner.Get() = nullptr;
}

```

