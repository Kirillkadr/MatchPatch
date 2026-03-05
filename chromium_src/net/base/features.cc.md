### match
```
...
#include <string>

 #include <vector>
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```
#include "base/feature_override.h"
#include "brave/net/dns/secure_dns_endpoints.h"

```

### match
```
...
 namespace net::features { ... 
 >>>  } ...  
```
### patch
```
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kEnableWebTransportDraft07, base::FEATURE_DISABLED_BY_DEFAULT},
    // Enable NIK-partitioning by default.
    {kPartitionConnectionsByNetworkIsolationKey,
     base::FEATURE_ENABLED_BY_DEFAULT},
    {kTpcdMetadataGrants, base::FEATURE_DISABLED_BY_DEFAULT},
    {kWaitForFirstPartySetsInit, base::FEATURE_DISABLED_BY_DEFAULT},
}});

BASE_FEATURE(kBraveEphemeralStorage,
             "EphemeralStorage",
             base::FEATURE_ENABLED_BY_DEFAULT);
BASE_FEATURE(kBraveEphemeralStorageKeepAlive,
             base::FEATURE_ENABLED_BY_DEFAULT);

const base::FeatureParam<int> kBraveEphemeralStorageKeepAliveTimeInSeconds = {
    &kBraveEphemeralStorageKeepAlive,
    "BraveEphemeralStorageKeepAliveTimeInSeconds", 30};

BASE_FEATURE(kBraveFirstPartyEphemeralStorage,
             base::FEATURE_ENABLED_BY_DEFAULT);

// Partition HSTS state storage by top frame site.
BASE_FEATURE(kBravePartitionHSTS,
             base::FEATURE_ENABLED_BY_DEFAULT);

// Enables HTTPS-Only Mode in Private Windows with Tor by default.
BASE_FEATURE(kBraveTorWindowsHttpsOnly,
             base::FEATURE_ENABLED_BY_DEFAULT);

// Enabled HTTPS by Default.
BASE_FEATURE(kBraveHttpsByDefault,
             "HttpsByDefault",
             base::FEATURE_ENABLED_BY_DEFAULT);

// When enabled, use a fallback DNS over HTTPS (DoH)
// provider when the current DNS provider does not offer Secure DNS.
BASE_FEATURE(kBraveFallbackDoHProvider,
             base::FEATURE_DISABLED_BY_DEFAULT);

constexpr base::FeatureParam<DohFallbackEndpointType>::Option
    kBraveFallbackDoHProviderEndpointOptions[] = {
        {DohFallbackEndpointType::kNone, "none"},
        {DohFallbackEndpointType::kQuad9, "quad9"},
        {DohFallbackEndpointType::kWikimedia, "wikimedia"},
        {DohFallbackEndpointType::kCloudflare, "cloudflare"}};
constexpr base::FeatureParam<DohFallbackEndpointType>
    kBraveFallbackDoHProviderEndpoint{
        &kBraveFallbackDoHProvider, "BraveFallbackDoHProviderEndpoint",
        DohFallbackEndpointType::kNone,
        &kBraveFallbackDoHProviderEndpointOptions};

// Add "Forget by default" cookie blocking mode which cleanups storage after a
// website is closed.
BASE_FEATURE(kBraveForgetFirstPartyStorage,
             base::FEATURE_ENABLED_BY_DEFAULT);

// Ephemeralize third party cookies set during redirects.
BASE_FEATURE(kBraveProvisionalTLDEphemeralLifetime,
             base::FEATURE_ENABLED_BY_DEFAULT);

const base::FeatureParam<int>
    kBraveForgetFirstPartyStorageStartupCleanupDelayInSeconds = {
        &kBraveForgetFirstPartyStorage,
        "BraveForgetFirstPartyStorageStartupCleanupDelayInSeconds", 5};

const base::FeatureParam<bool> kBraveForgetFirstPartyStorageByDefault = {
    &kBraveForgetFirstPartyStorage, "BraveForgetFirstPartyStorageByDefault",
    false};

```
