### match
```cpp
...
// found in the LICENSE file.
 #include "content/browser/gpu/gpu_process_host.h"
 
 >>> 
#include <stddef.h>

 ...
```
### patch
```cpp
#if BUILDFLAG(IS_WIN)
#include "sandbox/policy/features.h"
#include "sandbox/win/src/sandbox_policy.h"
#endif  // BUILDFLAG(IS_WIN)

```

### match
```cpp
...
 config->AddDllToUnload(L"cmsetac.dll"); 
 >>> 
 ...
```
### patch
```cpp
    #if BUILDFLAG(IS_WIN)
        config->AddDllToUnload(L"cmsetac.dll");
        config->SetShouldPatchModuleFileName(base::FeatureList::IsEnabled( \
        sandbox::policy::features::kModuleFileNamePatch))
    #endif  // BUILDFLAG(IS_WIN)

```

### match
```cpp
...

 int GpuProcessHost::GetIDForTesting() const { ... 
return process_->GetData().id;
 } 
 >>> 
 ...
```
### patch
```cpp
#if BUILDFLAG(IS_WIN)
void GpuProcessHost::DidGetExecutablePath(const std::string& path) {
  executable_path_ = path;
}
#endif  // BUILDFLAG(IS_WIN)

```

