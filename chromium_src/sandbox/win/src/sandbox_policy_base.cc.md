### match
```
...
#pragma allow_unsafe_buffers

 #endif 
 >>> 
 ... 
```
### patch
```
#include "sandbox/win/src/sandbox_policy_base.h"
#include "sandbox/win/src/policy_broker.h"

```

### match
```
...
 ResultCode PolicyBase::SetupAllInterceptions(TargetProcess& target) { ...   >>> 
 if 
 (!SetupBasicInterceptions(&manager, config()->is_csrss_connected()))  <<< ... 
return SBOX_ERROR_SETUP_BASIC_INTERCEPTIONS;
 ... } ...  
```
### patch
```
  if (!SetupBasicInterceptions(&manager, config()->is_csrss_connected(), config())(&manager, config()->is_csrss_connected()))

```

### match
```
...
 void PolicyBase::AddDelegateData(base::span<const uint8_t> data) { ... 
delegate_data_ =
      std::make_unique<std::vector<uint8_t>>(data.begin(), data.end());
 } 
 >>> 
 ... 
```
### patch
```
void ConfigBase::SetShouldPatchModuleFileName(bool b) {
  should_patch_module_filename_ = b;
}
bool ConfigBase::ShouldPatchModuleFileName() const {
  return should_patch_module_filename_;
}

```

