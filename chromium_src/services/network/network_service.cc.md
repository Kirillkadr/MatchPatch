### match
```
...
// found in the LICENSE file.
 #include "services/network/network_service.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```
#include "brave/net/dns/secure_dns_counter.h"
#include "services/network/public/mojom/network_service.mojom.h"

```

### match
```
...
 namespace network { ...   >>> 
 void 
 NetworkService::UpdateKeyPinsList 
 ( 
 mojom::PinListPtr pin_list 
 ,  <<< ... 
base::Time update_time
 ... ) ...  } ...  
```
### patch
```
void NetworkService::UpdateKeyPinsList_Unused(mojom::PinListPtr pin_list,

```

### match
```
...
 namespace network { ... 
 std::unique_ptr<DevtoolsDurableMessageWriter>
NetworkService::MaybeCreateDurableMessageWriter(
    const base::UnguessableToken& throttling_profile_id,
    const std::string& devtools_request_id) { ... 
return std::make_unique<MultipleDurableMessageWriterImpl>(
      std::move(messages));
 } 
 >>> 
 ... } ...  
```
### patch
```
void NetworkService::GetDnsRequestCountsAndReset(
    mojom::NetworkService::GetDnsRequestCountsAndResetCallback callback) {
  net::DnsRequestCounts counts =
      net::SecureDnsCounter::GetInstance()->GetCountsAndReset();
  std::move(callback).Run(
      mojom::DnsRequestCounts::New(counts.total_count, counts.upgraded_count));
}
void NetworkService::UpdateKeyPinsList(mojom::PinListPtr pin_list,
                                       base::Time update_time) {}

```

