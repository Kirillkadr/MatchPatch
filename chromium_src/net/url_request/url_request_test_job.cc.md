### match
```
...
#include <list>

 #include <memory>
 
 >>> 
#include "base/compiler_specific.h"

 ... 
```
### patch
```
#include "base/stl_util.h"

```

### match
```
...
 
 namespace net { ... 
bool URLRequestTestJob::ProcessOnePendingMessage() {
  if (GetPendingJobs().empty()) {
    return false;
  }

  URLRequestTestJob* next_job(GetPendingJobs().front());
  GetPendingJobs().pop_front();

  DCHECK(!next_job->auto_advance());  // auto_advance jobs should be in this q
  next_job->ProcessNextOperation();
  return true;
}
 } 
 // namespace net 
 >>> 
 ... 
```
### patch
```
namespace base {
template <class T, class Allocator, class Predicate>
size_t EraseIf(std::list<T, Allocator>& container, Predicate pred);  // NOLINT
}  // namespace base
// When building for iOS with XCode 11.3.1 the build fails because Erase is
// declared and defined earlier than EraseIf that's used in Erase. Putting a
// forward declaration here helps get around that. XCode 11.4.1 doesn't have
// this problem.
```

