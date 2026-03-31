### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "chrome/browser/net/stub_resolver_config_reader.h"

 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_BRAVE_VPN)
#include "brave/components/brave_vpn/common/features.h"
#endif

#if BUILDFLAG(IS_WIN) && BUILDFLAG(ENABLE_BRAVE_VPN)
namespace {

bool IsBraveVPNConnected(PrefService* local_state) {
  if (!base::FeatureList::IsEnabled(
          brave_vpn::features::kBraveVPNDnsProtection)) {
    return false;
  }
  return !local_state->GetString(prefs::kBraveVpnDnsConfig).empty();
}

bool ShouldOverride(net::SecureDnsMode secure_dns_mode,
                    PrefService* local_state,
                    SecureDnsConfig::ManagementMode management_mode,
                    bool is_managed) {
  if (!IsBraveVPNConnected(local_state))
    return false;
  if (secure_dns_mode == net::SecureDnsMode::kSecure)
    return false;
  if (management_mode != SecureDnsConfig::ManagementMode::kNoOverride ||
      is_managed) {
    // there is already a managed policy or parental control in place
    return false;
  }

  return true;
}

bool MaybeOverrideDnsClientEnabled(
    net::SecureDnsMode secure_dns_mode,
    bool insecure_dns_client_enabled,
    PrefService* local_state,
    SecureDnsConfig::ManagementMode management_mode,
    bool is_managed) {
  if (ShouldOverride(secure_dns_mode, local_state, management_mode,
                     is_managed)) {
    // disable the insecure client for doh
    return false;
  }

  return insecure_dns_client_enabled;
}

net::SecureDnsMode MaybeOverrideDnsMode(
    net::SecureDnsMode secure_dns_mode,
    PrefService* local_state,
    SecureDnsConfig::ManagementMode management_mode,
    bool is_managed) {
  if (ShouldOverride(secure_dns_mode, local_state, management_mode,
                     is_managed)) {
    return net::SecureDnsMode::kSecure;
  }
  return secure_dns_mode;
}

net::DnsOverHttpsConfig MaybeOverrideDnsConfig(
    net::SecureDnsMode secure_dns_mode,
    net::DnsOverHttpsConfig doh_config,
    PrefService* local_state,
    SecureDnsConfig::ManagementMode management_mode,
    bool is_managed) {
  if (ShouldOverride(secure_dns_mode, local_state, management_mode,
                     is_managed)) {
    return net::DnsOverHttpsConfig::FromStringLax(
        local_state->GetString(prefs::kBraveVpnDnsConfig));
  }
  return doh_config;
}

SecureDnsConfig::ManagementMode MaybeOverrideForcedManagementMode(
    net::SecureDnsMode secure_dns_mode,
    PrefService* local_state,
    SecureDnsConfig::ManagementMode management_mode,
    bool is_managed) {
  // Don't change management mode if the doh settings are
  // managed by policy or by parental controls
  if (is_managed ||
      management_mode != SecureDnsConfig::ManagementMode::kNoOverride)
    return management_mode;

  // Otherwise always block changes to the doh config while the VPN
  // is connected
  if (IsBraveVPNConnected(local_state))
    return SecureDnsConfig::ManagementMode::kDisabledManaged;

  return management_mode;
}

std::vector<net::IPEndPoint> MaybeOverrideFallbackDohNameservers(
    net::SecureDnsMode secure_dns_mode,
    PrefService* local_state,
    SecureDnsConfig::ManagementMode management_mode,
    bool is_managed,
    std::vector<net::IPEndPoint> fallback_doh_nameservers) {
  if (ShouldOverride(secure_dns_mode, local_state, management_mode,
                     is_managed)) {
    return std::vector<net::IPEndPoint>();
  }

  return fallback_doh_nameservers;
}

}  // namespace

#define SecureDnsConfig(SECURE_DNS_MODE, SECURE_DOH_CONFIG,                    \
                        FORCED_MANAGEMENT_MODE, FALLBACK_DOH_NAMESERVERS)      \
  SecureDnsConfig(                                                             \
      MaybeOverrideDnsMode(SECURE_DNS_MODE, local_state_,                      \
                           FORCED_MANAGEMENT_MODE, is_managed),                \
      MaybeOverrideDnsConfig(SECURE_DNS_MODE, SECURE_DOH_CONFIG, local_state_, \
                             FORCED_MANAGEMENT_MODE, is_managed),              \
      MaybeOverrideForcedManagementMode(SECURE_DNS_MODE, local_state_,         \
                                        FORCED_MANAGEMENT_MODE, is_managed),   \
      MaybeOverrideFallbackDohNameservers(SECURE_DNS_MODE, local_state_,       \
                                          FORCED_MANAGEMENT_MODE, is_managed,  \
                                          FALLBACK_DOH_NAMESERVERS))

#define ConfigureStubHostResolver(                                             \
    INSECURE_DNS_CLIENT_ENABLED, HAPPY_EYEBALLS_V3_ENABLED, SECURE_DNS_MODE,   \
    DNS_OVER_HTTPS_CONFIG, ADDITIONAL_DNS_TYPES_ENABLED,                       \
    FALLBACK_DOH_NAMESERVERS)                                                  \
  ConfigureStubHostResolver(                                                   \
      MaybeOverrideDnsClientEnabled(SECURE_DNS_MODE,                           \
                                    INSECURE_DNS_CLIENT_ENABLED, local_state_, \
                                    forced_management_mode, is_managed),       \
      HAPPY_EYEBALLS_V3_ENABLED,                                               \
      MaybeOverrideDnsMode(SECURE_DNS_MODE, local_state_,                      \
                           forced_management_mode, is_managed),                \
      MaybeOverrideDnsConfig(SECURE_DNS_MODE, DNS_OVER_HTTPS_CONFIG,           \
                             local_state_, forced_management_mode,             \
                             is_managed),                                      \
      ADDITIONAL_DNS_TYPES_ENABLED,                                            \
      MaybeOverrideFallbackDohNameservers(SECURE_DNS_MODE, local_state_,       \
                                          forced_management_mode, is_managed,  \
                                          FALLBACK_DOH_NAMESERVERS))

#endif  // BUILDFLAG(IS_WIN) && BUILDFLAG(ENABLE_BRAVE_VPN)

#define StubResolverConfigReader StubResolverConfigReader_ChromiumImpl

```

### match
```cpp
...
#include "base/notreached.h"

 #include "base/values.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/components/brave_vpn/common/buildflags/buildflags.h"
#include "build/buildflag.h"

```

### match
```cpp
...
void StubResolverConfigReader::OnAndroidOwnedStateCheckComplete(
    bool has_profile_owner,
    bool has_device_owner) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  android_has_owner_ = has_profile_owner || has_device_owner;
  // update the network service if the actual result is "true" to save time.
  if (android_has_owner_.value())
    UpdateNetworkService(false /* record_metrics */);
}
 #endif 
 >>> 
 ... 
```
### patch
```cpp
#undef StubResolverConfigReader
#if BUILDFLAG(IS_WIN) && BUILDFLAG(ENABLE_BRAVE_VPN)
#undef ConfigureStubHostResolver
#undef SecureDnsConfig
#endif  // BUILDFLAG(IS_WIN) && BUILDFLAG(ENABLE_BRAVE_VPN)

bool StubResolverConfigReader::ShouldDisableDohForManaged() {
  return false;
}
```

