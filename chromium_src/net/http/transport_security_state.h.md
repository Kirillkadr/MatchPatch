### match
```cpp
...
 
 # ifndef ... 
#include <string_view>

 #include <vector>
 
 >>> 
#include "base/functional/callback.h"

 ...
```
### patch
```cpp
#include "brave/net/http/partitioned_host_state_map.h"
#include "net/base/isolation_info.h"

```

### match
```cpp
...
 
 # ifndef ... 
 namespace 
 net 
 { 
 >>> 
namespace ct {
enum class CTPolicyCompliance;
}
 ... } ...
```
### patch
```cpp
class TransportSecurityState;
using TransportSecurityState_BraveImpl = TransportSecurityState;
#define TransportSecurityState TransportSecurityState_ChromiumImpl

```

### match
```cpp
...
 
 PKPStatus CheckPins(bool is_issued_by_known_root,
                      const TransportSecurityState::PKPState& pkp_state,
                      const std::vector<SHA256HashValue>& hashes);
 >>> 
 ...
```
### patch
```cpp
#undef TransportSecurityState

```

### match
```cpp
...
   >>> 
 STSStateMap enabled_sts_hosts_;  <<< 
 ...
```
### patch
```cpp
  STSStateMap enabled_sts_hosts_unused_;
  friend TransportSecurityState_BraveImpl;
  PartitionedHostStateMap<STSStateMap> enabled_sts_hosts_;

```

### match
```cpp
... 
 namespace net { ... 
 
 >>> 
  } ...
```
### patch
```cpp
class NET_EXPORT TransportSecurityState
    : public TransportSecurityState_ChromiumImpl {
 public:
  using TransportSecurityState_ChromiumImpl::
      TransportSecurityState_ChromiumImpl;

  SSLUpgradeDecision GetSSLUpgradeDecision(
      const NetworkAnonymizationKey& network_anonymization_key,
      const std::string& host,
      bool is_top_level_nav,
      const NetLogWithSource& net_log = NetLogWithSource());
  bool ShouldSSLErrorsBeFatal(
      const NetworkAnonymizationKey& network_anonymization_key,
      const std::string& host);
  bool ShouldUpgradeToSSL(
      const NetworkAnonymizationKey& network_anonymization_key,
      const std::string& host,
      bool is_top_level_nav,
      const NetLogWithSource& net_log = NetLogWithSource());
  bool AddHSTSHeader(const IsolationInfo& isolation_info,
                     std::string_view host,
                     std::string_view value);

  // This is used only for manual adding via net-internals page.
  void AddHSTS(std::string_view host,
               const base::Time& expiry,
               bool include_subdomains);
  // These are used in some places where no NIK is available.
  bool ShouldSSLErrorsBeFatal(const std::string& host);
  bool ShouldUpgradeToSSL(const std::string& host,
                          bool is_top_level_nav,
                          const NetLogWithSource& net_log = NetLogWithSource());
  bool GetDynamicSTSState(const std::string& host, STSState* result);
  bool DeleteDynamicDataForHost(const std::string& host);
};

```



