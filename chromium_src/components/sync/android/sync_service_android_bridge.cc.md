### match
```cpp
...
// found in the LICENSE file.
 #include "components/sync/android/sync_service_android_bridge.h"
 
 >>> 
#include <cstdint>

 ... 
```
### patch
```cpp
#include "components/sync/service/sync_user_settings.h"

```

### match
```cpp
...
 
 namespace syncer { ... 
>>> 
 void 
 SyncServiceAndroidBridge::KeepAccountSettingsPrefsOnlyForUsers 
 ( 
<<< 
const std::vector<std::string>& gaia_id_strings
 ... ) ...  } ...  
```
### patch
```cpp
void SyncServiceAndroidBridge::KeepAccountSettingsPrefsOnlyForUsers_Unused(

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void SyncServiceAndroidBridge::KeepAccountSettingsPrefsOnlyForUsers_Unused(
	const std::vector<std::string>& gaia_id_strings) { ... 
>>> 
 native_sync_service_->GetUserSettings()->KeepAccountSettingsPrefsOnlyForUsers 
 ( 
<<< 
...) ...  } ...  } ...  
```
### patch
```cpp
  native_sync_service_->GetUserSettings()->KeepAccountSettingsPrefsOnlyForUsers_Unused(

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void SyncServiceAndroidBridge::KeepAccountSettingsPrefsOnlyForUsers_Unused(
	const std::vector<std::string>& gaia_id_strings) { ... 
native_sync_service_->GetUserSettings()->KeepAccountSettingsPrefsOnlyForUsers_Unused(
		gaia_ids);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// Along with SyncUserSettings::KeepAccountSettingsPrefsOnlyForUsers_Unused
// makes this method do nothing.
// We need it on Android because Brave Browser doesn't use Google Account
// to run Brave Sync. Otherwise empty gaia_ids arrives to
// SyncTransportDataPrefs::KeepAccountSettingsPrefsOnlyForUsers, where
// "Clears all account-keyed preferences for all accounts that are NOT in
// `available_gaia_ids`." So all kSyncTransportDataPerAccount gets wiped.
// Then ValidateSyncTransportData at sync_engine_impl.cc fails and
// SyncEngineImpl::Initialize overwrites sync transport prefs. Device with new
// generated cache guid is sent to the chain and all other devices see the
// duplicated entry in addition to other possible mess.
// To avoid this, override with empty implementation.
void SyncServiceAndroidBridge::KeepAccountSettingsPrefsOnlyForUsers(
    JNIEnv* env,
    const base::android::JavaRef<jobjectArray>& gaia_ids) {}

```

