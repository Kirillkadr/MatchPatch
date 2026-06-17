### match
```cpp
...
 #include <vector>
 
 >>> 
 ...
```
### patch
```cpp
#include <optional>
#include "brave/components/constants/brave_services_key.h"
#include "components/update_client/protocol_serializer.h"

```

### match
```cpp
...
>>>
 base::flat_map<std::string, std::string> 
 BuildUpdateCheckExtraRequestHeaders 
 ( 
<<< 
...) ...
```
### patch
```cpp
base::flat_map<std::string, std::string> BuildUpdateCheckExtraRequestHeaders_ChromiumImpl(

```

### match
```cpp
...
  const int date_last_roll_call = metadata->GetDateLastRollCall(app_id);
  if (date_last_roll_call != kDateUnknown) {
    ping.date_last_roll_call = date_last_roll_call;
  } else {
    ping.days_since_last_roll_call = metadata->GetDaysSinceLastRollCall(app_id);
  }
  ping.ping_freshness = metadata->GetPingFreshness(app_id);

  return ping;

 } 
 >>> 
 ...
```
### patch
```cpp
base::flat_map<std::string, std::string> BuildUpdateCheckExtraRequestHeaders(
    const std::string& prod_id,
    const base::Version& browser_version,
    const std::vector<std::string>& ids,
    bool is_foreground) {
  auto headers = BuildUpdateCheckExtraRequestHeaders_ChromiumImpl(
      prod_id, browser_version, ids, is_foreground);
  headers.insert({"BraveServiceKey", BUILDFLAG(BRAVE_SERVICES_KEY)});
  return headers;
}

```

