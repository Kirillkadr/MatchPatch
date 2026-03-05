### match
```
...
#include <string>

 #include <utility>
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```
#include "base/containers/fixed_flat_map.h"
#include "base/feature_list.h"
#include "brave/net/dns/secure_dns_endpoints.h"
#include "net/base/features.h"
#include "net/dns/dns_util.h"
#include "net/dns/public/dns_over_https_server_config.h"
#include <vector>

```

### match
```
...
 namespace net { ... 
 namespace { ... 
 void UpdateConfigForDohUpgrade(DnsConfig* config) { ... 
 else { ... 
 DnsOverHttpsConfig ( ...   >>> 
 GetDohUpgradeServersFromNameservers(config->nameservers) 
 ) 
 ;  <<< ... } ...  } ...  } ...  } ...  
```
### patch
```
          MaybeAddFallbackDohServer(GetDohUpgradeServersFromNameservers(config->nameservers)));

```

### match
```
...
 namespace net { ... 
 std::unique_ptr<DnsClient> DnsClient::CreateClientForTesting(
    NetLog* net_log,
    const RandIntCallback& rand_int_callback) { ... 
return std::make_unique<DnsClientImpl>(net_log, rand_int_callback);
 } 
 >>> 
 ... } ...  
```
### patch
```
namespace {
constexpr auto kDohFallbackEndpointAddresses{
    base::MakeFixedFlatMap<DohFallbackEndpointType, const char*>({
        {DohFallbackEndpointType::kQuad9,
         "https://doh-brave.quad9.net/dns-query"},
        {DohFallbackEndpointType::kWikimedia,
         "https://wikimedia-dns.org/dns-query"},
        {DohFallbackEndpointType::kCloudflare,
         "https://brave.cloudflare-dns.com/dns-query"},
    })};

std::vector<DnsOverHttpsServerConfig> MaybeAddFallbackDohServer(
    std::vector<DnsOverHttpsServerConfig> doh_servers) {
  if (!base::FeatureList::IsEnabled(net::features::kBraveFallbackDoHProvider)) {
    return doh_servers;
  }
  static const DohFallbackEndpointType endpoint =
      net::features::kBraveFallbackDoHProviderEndpoint.Get();
  if (endpoint == DohFallbackEndpointType::kNone) {
    return doh_servers;
  }
  const char* endpointAddress = kDohFallbackEndpointAddresses.at(endpoint);
  auto fallbackDohServer =
      DnsOverHttpsServerConfig::FromString(endpointAddress);
  if (fallbackDohServer.has_value()) {
    doh_servers.push_back(fallbackDohServer.value());
  }
  return doh_servers;
}

}  // namespace

```

