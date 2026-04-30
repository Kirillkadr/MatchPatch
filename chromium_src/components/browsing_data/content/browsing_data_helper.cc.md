### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
#include "components/browsing_data/content/browsing_data_helper.h"

 ... 
```
### patch
```cpp
#include "components/browsing_data/content/browsing_data_helper.h"

```

### match
```cpp
...
#include "components/browsing_data/content/browsing_data_helper.h"

 #include "components/browsing_data/content/browsing_data_helper.h"
 
 >>> 
#include <algorithm>

 ... 
```
### patch
```cpp
#include "brave/components/content_settings/core/browser/brave_content_settings_browsing_data_utils.h"

```

### match
```cpp
...
>>>
 void 
 RemoveSiteSettingsData 
 ( 
 const base::Time& delete_begin 
 ,  <<< 
const base::Time& delete_end
 ... ) ...  
```
### patch
```cpp
void RemoveSiteSettingsData_ChromiumImpl(const base::Time& delete_begin,

```

### match
```cpp
...
 
 namespace browsing_data { ... 
 
 int GetUniqueThirdPartyCookiesHostCount(
    const GURL& top_frame_url,
    const BrowsingDataModel& browsing_data_model) { ... 
return unique_hosts.size();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void RemoveSiteSettingsData(const base::Time& delete_begin,
                            const base::Time& delete_end,
                            HostContentSettingsMap* host_content_settings_map) {
  RemoveSiteSettingsData_ChromiumImpl(delete_begin, delete_end,
                                      host_content_settings_map);
  BraveRemoveSiteSettingsData(delete_begin, delete_end,
                              host_content_settings_map);
}

```

