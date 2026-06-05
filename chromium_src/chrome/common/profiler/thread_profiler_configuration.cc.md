### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/common/profiler/thread_profiler_configuration.h"
 
 >>> 
#include <variant>

 ... 
```
### patch
```cpp
#include "chrome/common/profiler/thread_profiler_configuration.h"

```

### match
```cpp
...
>>>
 bool 
 ThreadProfilerConfiguration::IsProfilerEnabledForCurrentProcessAndThread 
 ( 
<<< 
sampling_profiler::ProfilerThreadType thread
 ... ) ...  
```
### patch
```cpp
bool ThreadProfilerConfiguration::IsProfilerEnabledForCurrentProcessAndThread_ChromiumImpl(

```

### match
```cpp
...
 
 bool ThreadProfilerConfiguration::IsProfilerEnabledForCurrentProcessAndThread_ChromiumImpl(
sampling_profiler::ProfilerThreadType thread) const { ... 
return IsProfilerEnabledForCurrentProcess() &&
         platform_configuration_->IsEnabledForThread(
             GetProfilerProcessType(*base::CommandLine::ForCurrentProcess()),
             thread, GetReleaseChannel());
 } 
 >>> 
 ... 
```
### patch
```cpp
bool ThreadProfilerConfiguration::IsProfilerEnabledForCurrentProcessAndThread(
    sampling_profiler::ProfilerThreadType thread) const {
  return false;
}

```

