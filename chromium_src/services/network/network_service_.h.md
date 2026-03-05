### match
```
...
 # ifndef ... 
#include <utility>

 #include <vector>
 
 >>> 
#include "base/component_export.h"

 ... 
```
### patch
```
#include "services/network/public/mojom/network_service.mojom.h"

```

### match
```
...
 # ifndef ... 
 namespace network { ... 
 const std::vector<net::IPEndPoint>& fallback_doh_nameservers 
 ) 
 override 
 ; 
 >>> 
 ... } ...  
```
### patch
```
  void GetDnsRequestCountsAndReset(GetDnsRequestCountsAndResetCallback callback) override;

```

### match
```
...
 # ifndef ... 
 namespace network { ... 
void SetCtEnforcementEnabled(
      bool enabled,
      SetCtEnforcementEnabledCallback callback) override;
 #endif 
 // BUILDFLAG(IS_CT_SUPPORTED) 
 >>> 
void UpdateKeyPinsList(mojom::PinListPtr pin_list,
                         base::Time update_time) override;
 ... } ...  
```
### patch
```
  void UpdateKeyPinsList_Unused(mojom::PinListPtr pin_list,
                           base::Time update_time);

```

