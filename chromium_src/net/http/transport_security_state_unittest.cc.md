### match
```
...
#include <string>

 #include <vector>
 
 >>> 
#include "base/base64.h"

 ...
```
### patch
```
#include "net/http/transport_security_state.h"
#include "net/base/network_anonymization_key.h"
#include "net/base/schemeful_site.h"
#include "url/gurl.h"
#include "url/origin.h"

```

### match
```
...
 namespace net { ... 
 namespace { ... 
 std::vector<SHA256HashValue> DeserializeHashes(
    base::span<const char* const> serialized_hashes) { ... 
return result;
 } 
 >>> 
 ... } ...  } ...
```
### patch
```
net::NetworkAnonymizationKey CreateNetworkAnonymizationKey(
    std::string_view top_frame_url) {
  net::SchemefulSite schemeful_site(url::Origin::Create(GURL(top_frame_url)));
  return net::NetworkAnonymizationKey::CreateFromFrameSite(schemeful_site,
                                                           schemeful_site);
}

```

### match
```
...
TransportSecurityState::STSState sts_state;
  ASSERT_TRUE(state.GetStaticSTSState("hsts.example.com", &sts_state));
  ASSERT_EQ(sts_state.upgrade_mode,
            TransportSecurityState::STSState::MODE_FORCE_HTTPS);
  ASSERT_TRUE(sts_state.include_subdomains);
  ASSERT_FALSE(state.GetStaticSTSState("dynamic.example.com", &sts_state));

  const base::Time current_time(base::Time::Now());
  const base::Time expiry = current_time + base::Seconds(1000);
>>> ...
```
### patch
```
  EXPECT_EQ(state.GetSSLUpgradeDecision(CreateNetworkAnonymizationKey("dynamic.example.com"),"dynamic.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kNoUpgrade);
  EXPECT_FALSE(state.ShouldUpgradeToSSL("dynamic.example.com",
                                        /*is_top_level_nav=*/true));

  EXPECT_EQ(state.GetSSLUpgradeDecision(CreateNetworkAnonymizationKey("hsts.example.com"),"hsts.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kStaticUpgrade);
  EXPECT_TRUE(
      state.ShouldUpgradeToSSL("hsts.example.com", /*is_top_level_nav=*/true));

  state.AddHSTS("dynamic.example.com", expiry, false);
  EXPECT_EQ(state.GetSSLUpgradeDecision(CreateNetworkAnonymizationKey("dynamic.example.com"),"dynamic.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kDynamicUpgrade);
  EXPECT_TRUE(state.ShouldUpgradeToSSL("dynamic.example.com",
                                       /*is_top_level_nav=*/true));

  // Dynamic state for a host that already has static state doesn't change the
  // decision.
  state.AddHSTS("subdomain.hsts.example.com", expiry, false);
  EXPECT_EQ(state.GetSSLUpgradeDecision(CreateNetworkAnonymizationKey("subdomain.hsts.example.com"),"subdomain.hsts.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kStaticUpgrade);
  EXPECT_TRUE(state.ShouldUpgradeToSSL("subdomain.hsts.example.com",
                                       /*is_top_level_nav=*/true));

```

### match
```
...
 namespace net { ... 
 TEST_F(TransportSecurityStateTest, StaticOrDynamicSource) { ... 
EXPECT_TRUE(state.ShouldUpgradeToSSL("subdomain.hsts.example.com",
		                                       /*is_top_level_nav=*/true));  >>> 
 EXPECT_EQ(state.GetSSLUpgradeDecision("dynamic.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kNoUpgrade); 
 EXPECT_FALSE(state.ShouldUpgradeToSSL("dynamic.example.com",
                                        /*is_top_level_nav=*/true)); 
 EXPECT_EQ(state.GetSSLUpgradeDecision("hsts.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kStaticUpgrade); 
 EXPECT_TRUE(
      state.ShouldUpgradeToSSL("hsts.example.com", /*is_top_level_nav=*/true)); 
 state.AddHSTS("dynamic.example.com", expiry, false); 
 EXPECT_EQ(state.GetSSLUpgradeDecision("dynamic.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kDynamicUpgrade); 
 EXPECT_TRUE(state.ShouldUpgradeToSSL("dynamic.example.com",
                                       /*is_top_level_nav=*/true)); 
 // Dynamic state for a host that already has static state doesn't change the 
 // decision. 
 state.AddHSTS("subdomain.hsts.example.com", expiry, false); 
 EXPECT_EQ(state.GetSSLUpgradeDecision("subdomain.hsts.example.com",
                                        /*is_top_level_nav=*/true),
            SSLUpgradeDecision::kStaticUpgrade); 
 EXPECT_TRUE(state.ShouldUpgradeToSSL("subdomain.hsts.example.com",
                                       /*is_top_level_nav=*/true));  <<< ... } ...  } ...  
```
### patch
```

```

