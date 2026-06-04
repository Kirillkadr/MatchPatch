### match
```
...
#include "components/crash/core/app/crash_export_thunks.h"

 #endif 
 >>> 
 ...
```
### patch
```
namespace {
// Split into two places to avoid patching:
// NOLINTNEXTLINE
// components\brave_vpn\browser\connection\win\brave_vpn_helper\brave_vpn_helper_crash_reporter_client.cc
// Need keep it in sync
constexpr char kBraveVPNHelperProcessType[] = "brave-vpn-helper";
// Split into two places to avoid patching:
// NOLINTNEXTLINE
// components\brave_vpn\browser\connection\wireguard\win\brave_vpn_wireguard_service\brave_wireguard_service_crash_reporter_client.cc
// Need keep it in sync
constexpr char kBraveWireguardProcessType[] = "brave-vpn-wireguard-service";
}  // namespace

```

### match
```
...
 >>> 
process_type == "GCPW Installer"
 ...
```
### patch
```
process_type == kBraveVPNHelperProcessType ||     
           process_type == kBraveWireguardProcessType ||

```