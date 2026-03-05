### match
```
...
 # ifndef ... 
#include <string>

 #include <string_view>
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```
#include "base/feature_list.h"
#include "base/metrics/field_trial_params.h"
#include "brave/net/dns/secure_dns_endpoints.h"
#include "net/base/net_export.h"

```

### match
```
...
 # ifndef ... 
 namespace net::features { ... 
 kDrainSpdySessionSynchronouslyOnRemoteEndpointDisconnect 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```
NET_EXPORT BASE_DECLARE_FEATURE(kBraveEphemeralStorage);
NET_EXPORT BASE_DECLARE_FEATURE(kBraveEphemeralStorageKeepAlive);
NET_EXPORT extern const base::FeatureParam<int>
    kBraveEphemeralStorageKeepAliveTimeInSeconds;
NET_EXPORT BASE_DECLARE_FEATURE(kBraveFirstPartyEphemeralStorage);
NET_EXPORT BASE_DECLARE_FEATURE(kBraveHttpsByDefault);
NET_EXPORT BASE_DECLARE_FEATURE(kBraveFallbackDoHProvider);
NET_EXPORT extern const base::FeatureParam<DohFallbackEndpointType>
    kBraveFallbackDoHProviderEndpoint;
NET_EXPORT BASE_DECLARE_FEATURE(kBravePartitionHSTS);
NET_EXPORT BASE_DECLARE_FEATURE(kBraveTorWindowsHttpsOnly);
NET_EXPORT BASE_DECLARE_FEATURE(kBraveForgetFirstPartyStorage);
NET_EXPORT BASE_DECLARE_FEATURE(kBraveProvisionalTLDEphemeralLifetime);
NET_EXPORT extern const base::FeatureParam<int>
    kBraveForgetFirstPartyStorageStartupCleanupDelayInSeconds;
NET_EXPORT extern const base::FeatureParam<bool>
    kBraveForgetFirstPartyStorageByDefault;

```

