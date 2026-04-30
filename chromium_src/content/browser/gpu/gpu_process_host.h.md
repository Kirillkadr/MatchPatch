### match
```cpp
...
 
 # ifndef ... 
#include "ui/gfx/gpu_extra_info.h"

 #include "url/gurl.h"
 
 >>> 
#if BUILDFLAG(IS_WIN)
#include "services/viz/privileged/mojom/gl/info_collection_gpu_service.mojom.h"
#endif
 ... 
```
### patch
```cpp
#include "build/build_config.h"
#include "components/viz/host/gpu_host_impl.h"
#include "services/viz/privileged/mojom/gl/gpu_host.mojom.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
void DidInitialize(
      const gpu::GPUInfo& gpu_info,
      const gpu::GpuFeatureInfo& gpu_feature_info,
      const std::optional<gpu::GPUInfo>& gpu_info_for_hardware_gpu,
      const std::optional<gpu::GpuFeatureInfo>&
          gpu_feature_info_for_hardware_gpu,
      const gfx::GpuExtraInfo& gpu_extra_info) override;
 void DidFailInitialize() override; 
 >>> 
void DidCreateContextSuccessfully() override;
 ... } ...  
```
### patch
```cpp

#if BUILDFLAG(IS_WIN)
// |executable_path_| used as storage for GPU process executable path.
  void DidGetExecutablePath(const std::string& path) override;

 public:
  const std::string& executable_path() const {
    return executable_path_;
  }

 private:
  std::string executable_path_;                           
  void DidFailInitialize() override;
#endif


```

