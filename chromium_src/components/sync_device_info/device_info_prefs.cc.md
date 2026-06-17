### match
```cpp
...
// Use of this source code is governed by a BSD-style license that can be
 // found in the LICENSE file. 
 >>> 
 ... 
```
### patch
```cpp
#include "components/sync_device_info/device_info_prefs.h"

```

### match
```cpp
...
 namespace 
 { 
 >>> 
// Preference name for storing recently used cache GUIDs and their timestamps
 ... } ...  
```
### patch
```cpp
// Preference name for storing the time when reset of progress token for devices
// was done. This happens when we need to re-fetch the devices which were
// expired and are hidden on the client but still present on the server.
constexpr char kResetDevicesProgressTokenTime[] =
    "brave_sync_v2.reset_devices_progress_token_time";

}  // namespace

bool DeviceInfoPrefs::IsResetDevicesProgressTokenDone() {
  base::Time time = pref_service_->GetTime(kResetDevicesProgressTokenTime);
  return !time.is_null();
}

void DeviceInfoPrefs::SetResetDevicesProgressTokenDone() {
  pref_service_->SetTime(kResetDevicesProgressTokenTime, base::Time::Now());
}

void DeviceInfoPrefs::RegisterProfilePrefs(PrefRegistrySimple* registry) {
  registry->RegisterTimePref(kResetDevicesProgressTokenTime, base::Time());
  RegisterProfilePrefs_ChromiumImpl(registry);
}
namespace {


```

### match
```cpp
...
 
 namespace syncer { ... 

namespace {

// Preference name for storing the time when reset of progress token for devices
		// was done. This happens when we need to re-fetch the devices which were
		// expired and are hidden on the client but still present on the server.
		constexpr char kResetDevicesProgressTokenTime[] =
		    "brave_sync_v2.reset_devices_progress_token_time";

		}  // namespace

		bool DeviceInfoPrefs::IsResetDevicesProgressTokenDone() {
		  base::Time time = pref_service_->GetTime(kResetDevicesProgressTokenTime);
		  return !time.is_null();
		}

		void DeviceInfoPrefs::SetResetDevicesProgressTokenDone() {
		  pref_service_->SetTime(kResetDevicesProgressTokenTime, base::Time::Now());
		}

		void DeviceInfoPrefs::RegisterProfilePrefs(PrefRegistrySimple* registry) {
		  registry->RegisterTimePref(kResetDevicesProgressTokenTime, base::Time());
		  RegisterProfilePrefs_ChromiumImpl(registry);
		}
		namespace {

		// Preference name for storing recently used cache GUIDs and their timestamps
// in days since Windows epoch. Most recent first.
const char kDeviceInfoRecentGUIDsWithTimestamps[] =
    "sync.local_device_guids_with_timestamp";

// Keys used in the dictionaries stored in prefs.
const char kCacheGuidKey[] = "cache_guid";
const char kTimestampKey[] = "timestamp";

// The max time a local device's cached GUIDs will be stored.
constexpr base::TimeDelta kMaxTimeDeltaLocalCacheGuidsStored = base::Days(10);

// The max number of local device most recent cached GUIDs that will be stored
// in preferences.
constexpr int kMaxLocalCacheGuidsStored = 30;

// Returns true iff |dict| is a dictionary with a cache GUID that is equal to
// |cache_guid|.
bool MatchesGuidInDictionary(const base::Value& dict,
                             const std::string& cache_guid) {
  if (!dict.is_dict()) {
    return false;
  }
  const std::string* v_cache_guid = dict.GetDict().FindString(kCacheGuidKey);
  return v_cache_guid && *v_cache_guid == cache_guid;
}

}  // namespace

// static

>>> 
 void 
 DeviceInfoPrefs::RegisterProfilePrefs(PrefRegistrySimple* registry) 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
void DeviceInfoPrefs::RegisterProfilePrefs_ChromiumImpl(PrefRegistrySimple* registry) {

```

