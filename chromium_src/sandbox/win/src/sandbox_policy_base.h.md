### match
```
...
 # ifndef ... 
#include <string_view>

 #include <vector>
 
 >>> 
#include "base/containers/span.h"

 ... 
```
### patch
```
#include "sandbox/win/src/sandbox_policy.h"

```

### match
```
...
 # ifndef ... 
 namespace sandbox { ... 
ConfigBase& operator=(const ConfigBase&) = delete;
 bool IsConfigured() const override; 
 >>> 
ResultCode SetTokenLevel(TokenLevel initial, TokenLevel lockdown) override;
 ... } ...  
```
### patch
```
  void SetShouldPatchModuleFileName(bool) override;
  bool ShouldPatchModuleFileName() const override;

```

### match
```
...
 # ifndef ... 
 namespace sandbox { ... 
 class ConfigBase final : public TargetConfig { ... 
// DCHECK_IS_ON()
 // Once true the configuration is frozen and can be applied to later policies. 
 >>> 
bool configured_ = false;
 ... } ...  } ...  
```
### patch
```
  bool should_patch_module_filename_ = false;

```

