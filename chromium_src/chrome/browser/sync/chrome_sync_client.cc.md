### match
```cpp
...
#include "base/task/sequenced_task_runner.h"

 #include "build/build_config.h"
 
 >>> 
#include "chrome/browser/metrics/chrome_metrics_service_accessor.h"

 ... 
```
### patch
```cpp
#include "build/buildflag.h"

```

### match
```cpp
...
#include "components/trusted_vault/trusted_vault_service.h"

 #include "content/public/browser/browser_thread.h"
 
 >>> 
namespace browser_sync {
namespace {

using content::BrowserThread;

#if BUILDFLAG(IS_WIN)
constexpr base::FilePath::CharType kLoopbackServerBackendFilename[] =
    FILE_PATH_LITERAL("profile.pb");
#endif  // BUILDFLAG(IS_WIN)

// A global variable is needed to detect multi-profile scenarios where more than
// one profile try to register a synthetic field trial. Rather than using a
// boolean, a struct is used to handle the case where the same profile is loaded
// multiple times and tries to register the very same synthetic field trial
// group (which shouldn't be considered a conflict).
struct ProfileAndGroupName {
  base::FilePath profile_base_name;
  std::string group_name;

  friend bool operator==(const ProfileAndGroupName& lhs,
                         const ProfileAndGroupName& rhs) = default;
};

std::optional<ProfileAndGroupName>& GetRegisteredProfileAndGroupName() {
  static base::NoDestructor<std::optional<ProfileAndGroupName>> value;
  return *value;
}

}  // namespace

ChromeSyncClient::ChromeSyncClient(
    const base::FilePath& profile_base_name,
    PrefService* pref_service,
    signin::IdentityManager* identity_manager,
    trusted_vault::TrustedVaultService* trusted_vault_service,
    syncer::SyncInvalidationsService* sync_invalidations_service,
    syncer::DeviceInfoSyncService* device_info_sync_service,
    syncer::DataTypeStoreService* data_type_store_service,
    supervised_user::FamilyLinkSettingsService* family_link_settings_service,
    std::unique_ptr<ExtensionsActivityMonitor> extensions_activity_monitor)
    : profile_base_name_(profile_base_name),
      pref_service_(pref_service),
      identity_manager_(identity_manager),
      trusted_vault_service_(trusted_vault_service),
      sync_invalidations_service_(sync_invalidations_service),
      family_link_settings_service_(family_link_settings_service),
      extensions_activity_monitor_(std::move(extensions_activity_monitor)),
      engine_factory_(this,
                      device_info_sync_service->GetDeviceInfoTracker(),
                      data_type_store_service->GetSyncDataPath()) {
  DCHECK_CURRENTLY_ON(BrowserThread::UI);
}

ChromeSyncClient::~ChromeSyncClient() = default;

PrefService* ChromeSyncClient::GetPrefService() {
  DCHECK_CURRENTLY_ON(BrowserThread::UI);
  return pref_service_;
}

signin::IdentityManager* ChromeSyncClient::GetIdentityManager() {
  DCHECK_CURRENTLY_ON(BrowserThread::UI);
  return identity_manager_;
}

base::FilePath ChromeSyncClient::GetLocalSyncBackendFolder() {
  base::FilePath local_sync_backend_folder =
      GetPrefService()->GetFilePath(syncer::prefs::kLocalSyncBackendDir);

#if BUILDFLAG(IS_WIN)
  if (local_sync_backend_folder.empty()) {
    if (!base::PathService::Get(chrome::DIR_ROAMING_USER_DATA,
                                &local_sync_backend_folder)) {
      SYSLOG(WARNING) << "Local sync can not get the roaming profile folder.";
      return base::FilePath();
    }
  }

  // This code as it is now will assume the same profile order is present on
  // all machines, which is not a given. It is to be defined if only the
  // Default profile should get this treatment or all profile as is the case
  // now.
  // TODO(pastarmovj): http://crbug.com/41291598 Decide if only the Default one
  // should be considered roamed. For now the code assumes all profiles are
  // created in the same order on all machines.
  local_sync_backend_folder =
      local_sync_backend_folder.Append(profile_base_name_);
  local_sync_backend_folder =
      local_sync_backend_folder.Append(kLoopbackServerBackendFilename);
#endif  // BUILDFLAG(IS_WIN)

  return local_sync_backend_folder;
}

trusted_vault::TrustedVaultClient* ChromeSyncClient::GetTrustedVaultClient() {
  return trusted_vault_service_->GetTrustedVaultClient(
      trusted_vault::SecurityDomainId::kChromeSync);
}

syncer::SyncInvalidationsService*
ChromeSyncClient::GetSyncInvalidationsService() {
  return sync_invalidations_service_;
}

scoped_refptr<syncer::ExtensionsActivity>
ChromeSyncClient::GetExtensionsActivity() {
  return extensions_activity_monitor_->GetExtensionsActivity();
}

syncer::SyncEngineFactory* ChromeSyncClient::GetSyncEngineFactory() {
  return &engine_factory_;
}

bool ChromeSyncClient::IsCustomPassphraseAllowed() {
  if (family_link_settings_service_) {
    return family_link_settings_service_->IsCustomPassphraseAllowed();
  }
  return true;
}

void ChromeSyncClient::RegisterTrustedVaultAutoUpgradeSyntheticFieldTrial(
    const syncer::TrustedVaultAutoUpgradeSyntheticFieldTrialGroup& group) {
  CHECK(group.is_valid());

  ProfileAndGroupName new_profile_and_group_name{profile_base_name_,
                                                 group.name()};

  std::optional<ProfileAndGroupName>& global_profile_and_group_name =
      GetRegisteredProfileAndGroupName();

  // If a group is previously set, it may imply that a different profile has
  // just been loaded, as this function is invoked at most once per profile.
  // However, on some platforms (e.g. Mac), the same profile can be closed and
  // loaded once again, and this case should not count as a conflict case.
  const bool multi_profile_conflict =
      global_profile_and_group_name.has_value() &&
      global_profile_and_group_name.value() != new_profile_and_group_name;

  // Use a special group name if a multi-profile conflict was detected.
  const std::string group_name =
      multi_profile_conflict
          ? syncer::TrustedVaultAutoUpgradeSyntheticFieldTrialGroup::
                GetMultiProfileConflictGroupName()
          : group.name();

  // If a conflict was detected, ensure that future runs of this function will
  // also report a conflict by using a pair that won't match future invocations
  // of this function.
  global_profile_and_group_name =
      multi_profile_conflict ? ProfileAndGroupName{base::FilePath(), group_name}
                             : new_profile_and_group_name;

  ChromeMetricsServiceAccessor::RegisterSyntheticFieldTrial(
      syncer::kTrustedVaultAutoUpgradeSyntheticFieldTrialName, group_name,
      variations::SyntheticTrialAnnotationMode::kCurrentLog);
}

bool ChromeSyncClient::IsMetricsAndCrashReportingEnabled() {
  return ChromeMetricsServiceAccessor::IsMetricsAndCrashReportingEnabled();
}

}
 ... 
```
### patch
```cpp
#include "extensions/buildflags/buildflags.h"

#if !BUILDFLAG(ENABLE_EXTENSIONS)
#define CHROME_BROWSER_WEB_APPLICATIONS_WEB_APP_PROVIDER_H_
#define CHROME_BROWSER_WEB_APPLICATIONS_WEB_APP_SYNC_BRIDGE_H_
#endif  // !BUILDFLAG(ENABLE_EXTENSIONS)

```

### match
```cpp
...
 
 namespace browser_sync { ... 
bool ChromeSyncClient::IsMetricsAndCrashReportingEnabled() {
  return ChromeMetricsServiceAccessor::IsMetricsAndCrashReportingEnabled();
}
 } 
 // namespace browser_sync 
 >>> 
 ... 
```
### patch
```cpp

#if !BUILDFLAG(ENABLE_EXTENSIONS)
#undef CHROME_BROWSER_WEB_APPLICATIONS_WEB_APP_SYNC_BRIDGE_H_
#undef CHROME_BROWSER_WEB_APPLICATIONS_WEB_APP_PROVIDER_H_
#endif  // !BUILDFLAG(ENABLE_EXTENSIONS)
```

