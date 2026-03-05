### match
```
...
#include <sddl.h>  // For ConvertSidToStringSidA.

 #include <memory>
 
 >>> 
#include "base/check.h"

 ... 
```
### patch
```
#include "base/command_line.h"
#include "brave/components/constants/brave_switches.h"

```

### match
```
...
 MachineIdStatus GetDeterministicMachineSpecificId(std::string* machine_id) { ... 
return MachineIdStatus::SUCCESS;
 } 
 >>> 
 ... 
```
### patch
```
namespace {
bool IsMachineIdDisabled() {
  return base::CommandLine::ForCurrentProcess()->HasSwitch(
      switches::kDisableMachineId);
}

}  // namespace
```

