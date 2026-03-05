### match
```
...
#include "net/base/lookup_string_in_fixed_set.h"

 #include <stdint.h>
 
 >>> 
#include <optional>

 ... 
```
### patch
```
#include "net/base/lookup_string_in_fixed_set.h"
#include <string_view>

#include "brave/components/brave_wallet/common/buildflags/buildflags.h"

```

### match
```
...
>>>
 std::optional<DomainRuleTags> 
 LookupSuffixInReversedSet 
 (  <<< ... 
base::span<const uint8_t> graph
 ... ) ...  
```
### patch
```
std::optional<DomainRuleTags> LookupSuffixInReversedSet_ChromiumImpl(

```

### match
```
...
 namespace net { ... 
 std::optional<DomainRuleTags> LookupSuffixInReversedSet_ChromiumImpl(
base::span<const uint8_t> graph,
    bool include_private,
    std::string_view host,
    size_t* suffix_length) { ... 
return result;
 } 
 >>> 
 ... } ...  
```
### patch
```
// Chromium pulls upstream public suffix list in effective_tld_names.dat and
// generate effective_tld_names.gperf from it. The list is processed by
// net/tools/dafsa/make_dafsa.py which will generate a byte array in
// effective_tld_names-reversed-inc.cc from the list to be used for comparison
// in the run-time. This function is the only function which looks up entries
// in the public suffix list, so we add our special case handling here to avoid
// patching effective_tld_names.gperf directly.
int LookupSuffixInReversedSet(base::span<const uint8_t> graph,
                              bool include_private,
                              std::string_view host,
                              size_t* suffix_length) {
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
  // Recognize .crypto(and other ud suffixes) and .eth as known TLDs for
  // decentralized DNS support. With this, when users type *.crypto or *.eth in
  // omnibox, it will be parsed as OmniboxInputType::URL input type instead of
  // OmniboxInputType::UNKNOWN, The first entry in the autocomplete list will be
  // URL instead of search.
  if (auto domain = decentralized_dns::GetUnstoppableDomainSuffix(host)) {
    *suffix_length = domain->size() - 1;
    return kDafsaFound;
  }
  if (host.ends_with(decentralized_dns::kEthDomain)) {
    *suffix_length = decentralized_dns::kEthDomain.size() - 1;
    return kDafsaFound;
  }
  if (host.ends_with(decentralized_dns::kSolDomain)) {
    *suffix_length = decentralized_dns::kSolDomain.size() - 1;
    return kDafsaFound;
  }
  if (include_private && host.ends_with(decentralized_dns::kDNSForEthDomain)) {
    *suffix_length = decentralized_dns::kDNSForEthDomain.size() - 1;
    return kDafsaFound;
  }
#endif  // BUILDFLAG(ENABLE_BRAVE_WALLET)

  return LookupSuffixInReversedSet_ChromiumImpl(graph, include_private, host,
                                                suffix_length);
}

```

