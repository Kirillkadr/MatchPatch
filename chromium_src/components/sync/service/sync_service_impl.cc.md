### match
```cpp
...
 #include <utility>
 
 >>> 
 ...
```
### patch
```cpp
#include "base/logging.h"
#include "brave/components/brave_sync/brave_sync_prefs.h"
#include "brave/components/sync/service/brave_sync_auth_manager.h"
#include "brave/components/sync/service/brave_sync_stopped_reporter.h"
#include "components/prefs/pref_service.h"
#include "components/sync/base/sync_util.h"

```

### match
```cpp
...
 namespace 
 syncer 
 { 
 >>> 
 ... } ...
```
### patch
```cpp
GURL BraveGetSyncServiceURL(const base::CommandLine& command_line,
                            version_info::Channel channel,
                            PrefService* prefs) {
  // Allow group policy to override sync service URL.
  // This has a higher priority than the --sync-url command-line param.
  // https://github.com/brave/brave-browser/issues/20431
  if (prefs && prefs->IsManagedPreference(brave_sync::kCustomSyncServiceUrl)) {
    std::string value(prefs->GetString(brave_sync::kCustomSyncServiceUrl));
    if (!value.empty()) {
      GURL custom_sync_url(value);
      // Provided URL must be HTTPS.
      if (custom_sync_url.is_valid() &&
          custom_sync_url.SchemeIs(url::kHttpsScheme)) {
        DVLOG(2) << "Sync URL specified via GPO: "
                 << prefs->GetString(brave_sync::kCustomSyncServiceUrl);
        return custom_sync_url;
      } else {
        LOG(WARNING) << "The following sync URL specified via GPO "
                     << "is invalid: " << value;
      }
    }
  }

  // Default logic.
  // See `GetSyncServiceURL` in `components/sync/base/sync_util.cc`
  return GetSyncServiceURL(command_line, channel);
}

// Reporting of sync errors is disabled in Brave to prevent the profile avatar
// button from providing visual feedback to the user.
SyncService::UserActionableError SyncServiceImpl::GetUserActionableError()
    const {
  return SyncService::UserActionableError::kNone;
}

```

### match
```cpp
...
>>>
 auth_manager_ 
 ( 
 std::make_unique<SyncAuthManager> 
 ( 
 identity_manager_ 
 , 
<<< 
/*delegate=*/
 ... ) ...  ) ...
```
### patch
```cpp
auth_manager_(std::make_unique<BraveSyncAuthManager>(identity_manager_,

```

### match
```cpp
...
>>> 
 GetSyncServiceURL(*base::CommandLine::ForCurrentProcess(), channel_) 
 ) 
 , 
<<< 
...
```
### patch
```cpp
BraveGetSyncServiceURL(*base::CommandLine::ForCurrentProcess(), channel_), sync_client_->GetPrefService())(),

```

### match
```cpp
...
>>>
 sync_stopped_reporter_ 
 = 
 std::make_unique<SyncStoppedReporter> 
 ( 
<<< 
...) ...  
```
### patch
```cpp
  sync_stopped_reporter_ = std::make_unique<BraveSyncStoppedReporter>(

```

### match
```cpp
...
 
 namespace syncer { ... 

GURL BraveGetSyncServiceURL(const base::CommandLine& command_line,
	                            version_info::Channel channel,
	                            PrefService* prefs) {
	  // Allow group policy to override sync service URL.
	  // This has a higher priority than the --sync-url command-line param.
	  // https://github.com/brave/brave-browser/issues/20431
	  if (prefs && prefs->IsManagedPreference(brave_sync::kCustomSyncServiceUrl)) {
	    std::string value(prefs->GetString(brave_sync::kCustomSyncServiceUrl));
	    if (!value.empty()) {
	      GURL custom_sync_url(value);
	      // Provided URL must be HTTPS.
	      if (custom_sync_url.is_valid() &&
	          custom_sync_url.SchemeIs(url::kHttpsScheme)) {
	        DVLOG(2) << "Sync URL specified via GPO: "
	                 << prefs->GetString(brave_sync::kCustomSyncServiceUrl);
	        return custom_sync_url;
	      } else {
	        LOG(WARNING) << "The following sync URL specified via GPO "
	                     << "is invalid: " << value;
	      }
	    }
	  }

	  // Default logic.
	  // See `GetSyncServiceURL` in `components/sync/base/sync_util.cc`
	  return GetSyncServiceURL(command_line, channel);
	}

	// Reporting of sync errors is disabled in Brave to prevent the profile avatar
	// button from providing visual feedback to the user.
	SyncService::UserActionableError SyncServiceImpl::GetUserActionableError()
	    const {
	  return SyncService::UserActionableError::kNone;
	}

	namespace {

BASE_FEATURE(kSyncUnsubscribeFromTypesWithPermanentErrors,
             base::FEATURE_ENABLED_BY_DEFAULT);

#if BUILDFLAG(IS_ANDROID)
constexpr int kMinGmsVersionCodeWithCustomPassphraseApi = 235204000;

// Keep in sync with the corresponding string in
// ExplicitPassphrasePlatformClientTest.java
constexpr char kIgnoreMinGmsVersionWithPassphraseSupportForTest[] =
    "ignore-min-gms-version-with-passphrase-support-for-test";
#endif  // BUILDFLAG(IS_ANDROID)

// The initial state of sync, for the Sync.InitialState2 histogram. Even if
// this value indicates that sync (the feature or the transport) can start, the
// startup might fail for reasons such as network issues, or the version of
// Chrome being too old.
// These values are persisted to logs. Entries should not be renumbered and
// numeric values should never be reused.
// LINT.IfChange(SyncInitialState)
enum SyncInitialState {
  // Sync-the-feature can attempt to start up.
  kFeatureCanStart = 0,
  // There is no signed in user, so neither feature nor transport can start.
  kNotSignedIn = 1,
  // The user has disabled Sync-the-feature, but the initial setup has been
  // completed. This should be very rare; it can happen after a
  // reset-via-dashboard on ChromeOS.
  kFeatureNotRequested = 2,
  // The user has not enabled Sync-the-feature. This is the expected state for
  // a Sync-the-transport (signed-in non-syncing) user.
  kFeatureNotRequestedNotSetup = 3,
  // The user has enabled Sync-the-feature, but has not completed the initial
  // setup. This should be rare; it can happen if the initial setup got
  // interrupted e.g. by a crash.
  kFeatureNotSetup = 4,
  // Sync (both feature and transport) is disallowed by enterprise policy.
  kNotAllowedByPolicy = 5,
  kObsoleteNotAllowedByPlatform = 6,
  kMaxValue = kObsoleteNotAllowedByPlatform
};
// LINT.ThenChange(/tools/metrics/histograms/metadata/sync/enums.xml:SyncInitialState)

// These values are persisted to logs. Entries should not be renumbered and
// numeric values should never be reused.
enum class DownloadStatusWaitingForUpdatesReason {
  kRefreshTokensNotLoaded = 0,
  kSyncEngineNotInitialized = 1,
  kDataTypeNotActive = 2,
  kInvalidationsNotInitialized = 3,
  kIncomingInvalidation = 4,
  kPollRequestScheduled = 5,

  kMaxValue = kPollRequestScheduled
};

void RecordSyncInitialState(SyncService::DisableReasonSet disable_reasons,
                            bool is_sync_feature_requested,
                            bool initial_sync_feature_setup_complete) {
  SyncInitialState sync_state = kFeatureCanStart;
  if (disable_reasons.Has(SyncService::DISABLE_REASON_NOT_SIGNED_IN)) {
    sync_state = kNotSignedIn;
  } else if (disable_reasons.Has(
                 SyncService::DISABLE_REASON_ENTERPRISE_POLICY)) {
    sync_state = kNotAllowedByPolicy;
  } else if (!is_sync_feature_requested) {
    if (initial_sync_feature_setup_complete) {
      sync_state = kFeatureNotRequested;
    } else {
      sync_state = kFeatureNotRequestedNotSetup;
    }
  } else if (!initial_sync_feature_setup_complete) {
    sync_state = kFeatureNotSetup;
  }
  base::UmaHistogramEnumeration("Sync.InitialState2", sync_state);
}

EngineComponentsFactory::Switches EngineSwitchesFromCommandLine() {
  EngineComponentsFactory::Switches factory_switches = {
      EngineComponentsFactory::BACKOFF_NORMAL,
      /*force_short_nudge_delay_for_test=*/false};

  const base::CommandLine* cl = base::CommandLine::ForCurrentProcess();
  if (cl->HasSwitch(kSyncShortInitialRetryOverride)) {
    factory_switches.backoff_override =
        EngineComponentsFactory::BACKOFF_SHORT_INITIAL_RETRY_OVERRIDE;
  }
  if (cl->HasSwitch(kSyncShortNudgeDelayForTest)) {
    factory_switches.force_short_nudge_delay_for_test = true;
  }
  return factory_switches;
}

base::TimeDelta GetDeferredInitDelay() {
  if (base::FeatureList::IsEnabled(kDeferredSyncStartupCustomDelay)) {
    return base::Seconds(kDeferredSyncStartupCustomDelayInSeconds.Get());
  }

  const base::CommandLine* cmdline = base::CommandLine::ForCurrentProcess();
  if (cmdline->HasSwitch(kSyncDeferredStartupTimeoutSeconds)) {
    int timeout = 0;
    if (base::StringToInt(
            cmdline->GetSwitchValueASCII(kSyncDeferredStartupTimeoutSeconds),
            &timeout)) {
      DCHECK_GE(timeout, 0);
      return base::Seconds(timeout);
    }
  }
  return base::Seconds(10);
}

void MaybeClearAccountKeyedPreferences(
    signin::IdentityManager* identity_manager,
    const signin::AccountsInCookieJarInfo& accounts_in_cookie_jar_info,
    SyncUserSettingsImpl& user_settings) {
#if !BUILDFLAG(IS_IOS) && !BUILDFLAG(IS_ANDROID)
  if (accounts_in_cookie_jar_info.AreAccountsFresh()) {
    // Clear settings for accounts no longer in the cookie jar. On Android
    // and iOS this is done when the account is removed from the OS instead.
    std::vector<GaiaId> gaia_ids =
        base::ToVector(signin::GetAllGaiaIdsForKeyedPreferences(
            identity_manager, accounts_in_cookie_jar_info));
    user_settings.KeepAccountSettingsPrefsOnlyForUsers(gaia_ids);
  }
#endif  // !BUILDFLAG(IS_IOS) && !BUILDFLAG(IS_ANDROID)
}

}  // namespace

SyncServiceImpl::InitParams::InitParams() = default;
SyncServiceImpl::InitParams::InitParams(InitParams&& other) = default;
SyncServiceImpl::InitParams::~InitParams() = default;

SyncServiceImpl::SyncServiceImpl(InitParams init_params)
    : sync_client_(std::move(init_params.sync_client)),
      create_http_post_provider_factory_(
          std::move(init_params.create_http_post_provider_factory)),
      os_crypt_async_(init_params.os_crypt_async),
      sync_prefs_(sync_client_->GetPrefService()),
      identity_manager_(sync_prefs_.IsLocalSyncEnabled()
                            ? nullptr
                            : sync_client_->GetIdentityManager()),
      auth_manager_(std::make_unique<BraveSyncAuthManager>(identity_manager_,
/*delegate=*/this)),
      channel_(init_params.channel),
      debug_identifier_(std::move(init_params.debug_identifier)),
      sync_service_url_(
          BraveGetSyncServiceURL(*base::CommandLine::ForCurrentProcess(), channel_), sync_client_->GetPrefService())(),
crypto_(this, sync_client_->GetTrustedVaultClient()),
      url_loader_factory_(std::move(init_params.url_loader_factory)),
      network_connection_tracker_(
          std::move(init_params.network_connection_tracker)) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  DCHECK(sync_client_);
  DCHECK(IsLocalSyncEnabled() || identity_manager_ != nullptr);
  CHECK(os_crypt_async_);

  // If Sync is disabled via command line flag, then SyncServiceImpl
  // shouldn't be instantiated.
  DCHECK(IsSyncAllowedByFlag());

    sync_stopped_reporter_ = std::make_unique<BraveSyncStoppedReporter>(
sync_service_url_, MakeUserAgentForSync(channel_), url_loader_factory_);

  if (identity_manager_) {
    identity_manager_observation_.Observe(identity_manager_);
  }

  observers_.emplace();

  // Based on the information cached in preferences, it might be required to
  // register a synthetic field trial group. This should be done as early as
  // possible to avoid untagged metrics if they get logged before other events
  // like sync engine initialization, which could take arbitrarily long (e.g.
  // persistent auth error). Task-posting is involved to avoid infinite
  // recursions if the implementation in SyncClient leads to
  // accessing/constructing SyncService.
  base::SequencedTaskRunner::GetCurrentDefault()->PostTask(
      FROM_HERE,
      base::BindOnce(
          &SyncServiceImpl::RegisterTrustedVaultSyntheticFieldTrialsIfNecessary,
          weak_factory_.GetWeakPtr()));
}

void SyncServiceImpl::RegisterTrustedVaultSyntheticFieldTrialsIfNecessary() {
  if (trusted_vault_auto_upgrade_synthetic_field_trial_registered_) {
    // Registration function already invoked. It cannot be invoked twice, as
    // runtime changes to the group assignment is not supported (e.g. signout).
    return;
  }

  const sync_pb::TrustedVaultAutoUpgradeExperimentGroup proto =
      sync_prefs_.GetCachedTrustedVaultAutoUpgradeExperimentGroup().value_or(
          sync_pb::TrustedVaultAutoUpgradeExperimentGroup());

  const TrustedVaultAutoUpgradeSyntheticFieldTrialGroup group =
      TrustedVaultAutoUpgradeSyntheticFieldTrialGroup::FromProto(proto);

  if (!group.is_valid()) {
    // Broadcasting an invalid group isn't allowed, as it would otherwise use
    // the only chance to invoke the registration function below, which may only
    // be invoked once.
    return;
  }

  trusted_vault_auto_upgrade_synthetic_field_trial_registered_ = true;
  sync_client_->RegisterTrustedVaultAutoUpgradeSyntheticFieldTrial(group);
}

SyncServiceImpl::~SyncServiceImpl() {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  // Shutdown() should have been called before destruction.
  DCHECK(!engine_);
}

void SyncServiceImpl::Initialize(DataTypeController::TypeVector controllers) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);

  data_type_manager_ = std::make_unique<DataTypeManagerImpl>(
      std::move(controllers), &crypto_, this);

  // It's safe to pass a raw ptr, since SyncServiceImpl outlives
  // SyncUserSettingsImpl.
  user_settings_ = std::make_unique<SyncUserSettingsImpl>(
      /*delegate=*/this, &crypto_, &sync_prefs_,
      data_type_manager_->GetRegisteredDataTypes());

  if (!IsLocalSyncEnabled()) {
    auth_manager_->RegisterForAuthNotifications();

    // Trigger a refresh when additional data types get enabled for
    // invalidations. This is needed to get the latest data after subscribing
    // for the updates.
    sync_client_->GetSyncInvalidationsService()
        ->SetCommittedAdditionalInterestedDataTypesCallback(base::BindRepeating(
            &SyncServiceImpl::TriggerRefresh, weak_factory_.GetWeakPtr(),
            TriggerRefreshSource::kSyncInvalidationsService));

    // TODO(crbug.com/40257467): revisit this logic. IsSignedIn() doesn't feel
    // the right condition to check.
    if (IsSignedIn()) {
      // Start receiving invalidations as soon as possible since GCMDriver drops
      // incoming FCM messages otherwise. The messages will be collected by
      // SyncInvalidationsService until sync engine is initialized and ready to
      // handle invalidations.
      sync_client_->GetSyncInvalidationsService()->StartListening();
    }
  }

  // *After* setting up `auth_manager_`, run pref migrations that depend on
  // the account state.
  sync_prefs_.MaybeMigratePrefsForSyncToSigninPart1(
      GetSyncAccountStateForPrefs(), GetAccountInfo().gaia);
  sync_prefs_.MaybeMigrateCustomPassphrasePref(GetAccountInfo().gaia);

  // Update selected types prefs if a policy is applied.
  sync_prefs_policy_handler_ = std::make_unique<SyncPrefsPolicyHandler>(this);

  // If sync is disabled permanently, clean up old data that may be around (e.g.
  // crash during signout).
  if (HasDisableReason(DISABLE_REASON_ENTERPRISE_POLICY)) {
    StopAndClear(ResetEngineReason::kEnterprisePolicy);
#if BUILDFLAG(IS_CHROMEOS)
    // Disable OS data types to avoid automatic local data upload upon policy
    // removal, as OS data types do not support dual storage with UNO.
    if (!HasSyncConsent() && IsReplaceSyncPromosWithSignInPromosEnabled()) {
      user_settings_->SetSelectedOsTypes(/*sync_all_os_types=*/false,
                                         UserSelectableOsTypeSet());
    } else {
      // On ChromeOS Ash, sync-the-feature stays disabled even after the policy
      // is removed, for historic reasons. It is unclear if this behavior is
      // optional, because it is indistinguishable from the
      // sync-reset-via-dashboard case. It can be resolved by invoking
      // ClearSyncFeatureDisabledViaDashboard().
      user_settings_->SetSyncFeatureDisabledViaDashboard();
    }
#endif  // BUILDFLAG(IS_CHROMEOS)
  } else if (HasDisableReason(DISABLE_REASON_NOT_SIGNED_IN)) {
    // On ChromeOS-Ash, signout is not possible, so it's not necessary to handle
    // this case.
    // TODO(crbug.com/40272157): It *should* be harmless to handle this case on
    // ChromeOS-Ash since it's supposedly unreachable, *but* during the very
    // first startup of a fresh profile, the signed-in account isn't known yet
    // at this point (see also https://crbug.com/1458701#c7).
#if !BUILDFLAG(IS_CHROMEOS)
    StopAndClear(ResetEngineReason::kNotSignedIn);
#endif
  }

  const bool is_sync_feature_requested_for_metrics =
      IsLocalSyncEnabled() ||
#if BUILDFLAG(IS_CHROMEOS)
      !user_settings_->IsSyncFeatureDisabledViaDashboard();
#else
      HasSyncConsent();
#endif  // BUILDFLAG(IS_CHROMEOS)

  // Note: We need to record the initial state *after* calling
  // RegisterForAuthNotifications(), because before that the authenticated
  // account isn't initialized.
  RecordSyncInitialState(GetDisableReasons(),
                         is_sync_feature_requested_for_metrics,
                         user_settings_->IsInitialSyncFeatureSetupComplete());

  // Call Stop() on controllers for non-preferred types to clear metadata.
  // This allows clearing metadata for types disabled in previous run early-on
  // during initialization.
  data_type_manager_->ClearMetadataWhileStoppedExceptFor(
      GetPreferredDataTypes());

  if (IsEngineAllowedToRun()) {
    if (!sync_client_->GetSyncEngineFactory()
             ->HasTransportDataIncludingFirstSync(
                 signin::GaiaIdHash::FromGaiaId(GetAccountInfo().gaia))) {
      // Sync never initialized before on this profile, so let's try immediately
      // the very first time. This is particularly useful for Chrome Ash (where
      // the user is signed in to begin with) and local sync (where sign-in
      // state doesn't matter to start the engine).
      TryStart();
    } else {
      // Defer starting the engine, for browser startup performance. If another
      // TryStart() happens in the meantime, this deferred task will no-op.
      deferring_first_start_since_ = base::Time::Now();
      base::SequencedTaskRunner::GetCurrentDefault()->PostDelayedTask(
          FROM_HERE,
          base::BindOnce(&SyncServiceImpl::TryStart,
                         weak_factory_.GetWeakPtr()),
          GetDeferredInitDelay());
    }
  }

  sync_status_recorder_ =
      std::make_unique<SyncFeatureStatusForMigrationsRecorder>(
          sync_client_->GetPrefService(), this);

  local_data_migration_item_queue_ =
      std::make_unique<LocalDataMigrationItemQueue>(this,
                                                    data_type_manager_.get());

  device_statistics_scheduler_ = std::make_unique<DeviceStatisticsScheduler>(
      /*delegate=*/this, sync_client_->GetPrefService(),
      sync_client_->GetIdentityManager(), sync_service_url_);
}

void SyncServiceImpl::StartSyncingWithServer() {
  if (engine_) {
    engine_->StartSyncingWithServer();
  }
  if (IsLocalSyncEnabled()) {
    TriggerRefresh(TriggerRefreshSource::kLocalSync, DataTypeSet::All());
  }
}

DataTypeSet SyncServiceImpl::GetRegisteredDataTypesForTest() const {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  CHECK_IS_TEST();
  return data_type_manager_->GetRegisteredDataTypes();
}

bool SyncServiceImpl::HasAnyModelErrorForTest(DataTypeSet types) const {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  CHECK_IS_TEST();
  CHECK(data_type_manager_);

  for (DataType type : types) {
    DataTypeController* controller =
        data_type_manager_->GetControllerForTest(type);  // IN-TEST
    if (controller && controller->state() == DataTypeController::FAILED) {
      return true;
    }
  }
  return false;
}

void SyncServiceImpl::GetThrottledDataTypesForTest(
    base::OnceCallback<void(DataTypeSet)> cb) const {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  CHECK_IS_TEST();

  if (!engine_ || !engine_->IsInitialized()) {
    std::move(cb).Run(DataTypeSet());
    return;
  }

  engine_->GetThrottledDataTypesForTest(std::move(cb));  // IN-TEST
}

size_t SyncServiceImpl::GetQueuedLocalDataMigrationItemCountForTest() const {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  CHECK_IS_TEST();

  return local_data_migration_item_queue_
      ->GetItemsCountForTesting();  // IN-TEST
}

// static
ShutdownReason SyncServiceImpl::ShutdownReasonForResetEngineReason(
    ResetEngineReason reset_reason) {
  switch (reset_reason) {
    case ResetEngineReason::kShutdown:
      return ShutdownReason::BROWSER_SHUTDOWN_AND_KEEP_DATA;
    case ResetEngineReason::kCredentialsChanged:
      return ShutdownReason::STOP_SYNC_AND_KEEP_DATA;
    case ResetEngineReason::kUnrecoverableError:
    case ResetEngineReason::kDisabledAccount:
    case ResetEngineReason::kResetLocalData:
    case ResetEngineReason::kUpgradeClientError:
    case ResetEngineReason::kNotSignedIn:
    case ResetEngineReason::kEnterprisePolicy:
    case ResetEngineReason::kDisableSyncOnClient:
      return ShutdownReason::DISABLE_SYNC_AND_CLEAR_DATA;
  }
}

bool SyncServiceImpl::ShouldClearTransportDataForAccount(
    ResetEngineReason reset_reason) {
  switch (reset_reason) {
    case ResetEngineReason::kShutdown:
    case ResetEngineReason::kDisabledAccount:
    case ResetEngineReason::kUpgradeClientError:
    case ResetEngineReason::kCredentialsChanged:
    case ResetEngineReason::kNotSignedIn:
    case ResetEngineReason::kEnterprisePolicy:
      // Regular/benign cases; no need to clear.
      return false;
    case ResetEngineReason::kUnrecoverableError:
    case ResetEngineReason::kResetLocalData:
    case ResetEngineReason::kDisableSyncOnClient:
      // Weird error, or explicit request to reset. Clear transport data to
      // start over fresh.
      return true;
  }
}

bool SyncServiceImpl::IsEngineAllowedToRun() const {
  return GetDisableReasons().empty() && !auth_manager_->IsSyncPaused();
}

void SyncServiceImpl::OnProtocolEvent(const ProtocolEvent& event) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  for (ProtocolEventObserver& observer : protocol_event_observers_) {
    observer.OnProtocolEvent(event);
  }
}

void SyncServiceImpl::OnDataTypeRequestsSyncStartup(DataType type) {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  DCHECK(UserTypes().Has(type));

  if (!GetPreferredDataTypes().Has(type)) {
    // We can get here as datatype SyncableServices are typically wired up
    // to the native datatype even if sync isn't enabled.
    DVLOG(1) << "Dropping sync startup request because type "
             << DataTypeToDebugString(type) << "not enabled.";
    return;
  }

  if (engine_) {
    DVLOG(1) << "A data type requested sync startup, but it looks like "
                "something else beat it to the punch.";
    return;
  }

  TryStart();
}

void SyncServiceImpl::TryStart() {
  CHECK(os_crypt_async_);
  // It's possible for this to be called multiple times before the callback
  // runs (e.g. if the user signs out and back in again). This is safe, as
  // OSCryptAsync will just queue the callbacks and run them once the
  // encryptor is available. The first call to TryStartImpl() that succeeds
  // will create the engine, and subsequent ones will be no-ops.
  // TODO(crbug.com/514283732): Now that Encryptor is a refcounted object, we
  // can the barrier is probably not needed anymore. Investigate if it can be
  // removed.
  auto barrier =
      base::BarrierCallback<scoped_refptr<os_crypt_async::Encryptor>>(
          2,
          base::BindOnce(&SyncServiceImpl::TryStartImpl,
                         weak_factory_.GetWeakPtr(), base::TimeTicks::Now()));

  // One instance of Encryptor is needed for SyncServiceImpl and one for
  // SyncEngine.
  os_crypt_async_->GetInstance(barrier);
  os_crypt_async_->GetInstance(barrier);
}

void SyncServiceImpl::TryStartImpl(
    base::TimeTicks try_start_time,
    std::vector<scoped_refptr<os_crypt_async::Encryptor>> encryptors) {
  base::Time deferral_time;
  std::swap(deferring_first_start_since_, deferral_time);

  if (engine_ || !IsEngineAllowedToRun()) {
    return;
  }

  CHECK_EQ(encryptors.size(), 2u);

  base::UmaHistogramTimes("Sync.EncryptorReceivedTime",
                          base::TimeTicks::Now() - try_start_time);

  // One instance of Encryptor is needed for SyncServiceImpl and one for
  // SyncEngine.
  crypto_.SetEncryptor(std::move(encryptors[0]));

  if (!deferral_time.is_null()) {
    base::UmaHistogramCustomTimes("Sync.Startup.TimeDeferred2",
                                  base::Time::Now() - deferral_time,
                                  base::Seconds(0), base::Minutes(2), 60);
  }

  const CoreAccountInfo authenticated_account_info = GetAccountInfo();

  if (IsLocalSyncEnabled()) {
    // With local sync (roaming profiles) there is no identity manager and hence
    // `authenticated_account_info` is empty. This is required for
    // IsLocalSyncTransportDataValid() to work properly.
    DCHECK(authenticated_account_info.gaia.empty());
    DCHECK(authenticated_account_info.account_id.empty());
  } else {
    // Except for local sync (roaming profiles), the user must be signed in for
    // sync to start.
    DCHECK(!authenticated_account_info.gaia.empty());
    DCHECK(!authenticated_account_info.account_id.empty());
  }

  engine_ = sync_client_->GetSyncEngineFactory()->CreateSyncEngine(
      debug_identifier_,
      signin::GaiaIdHash::FromGaiaId(authenticated_account_info.gaia),
      sync_client_->GetSyncInvalidationsService());
  DCHECK(engine_);

  // Clear any old errors the first time sync starts.
  if (!user_settings_->IsInitialSyncFeatureSetupComplete()) {
    last_actionable_error_ = SyncProtocolError();
  }

  SyncEngine::InitParams params;
  params.host = this;
  params.encryption_observer_proxy = crypto_.GetEncryptionObserverProxy();

  params.extensions_activity = sync_client_->GetExtensionsActivity();
  params.service_url = sync_service_url_;
  params.http_factory_getter = base::BindOnce(
      create_http_post_provider_factory_override_for_test_.value_or(
          create_http_post_provider_factory_),
      MakeUserAgentForSync(channel_), url_loader_factory_->Clone());
  params.authenticated_account_info = authenticated_account_info;

  params.sync_manager_factory =
      std::make_unique<SyncManagerFactory>(network_connection_tracker_);
  if (sync_prefs_.IsLocalSyncEnabled()) {
    params.enable_local_sync_backend = true;
    params.local_sync_backend_folder =
        sync_client_->GetLocalSyncBackendFolder();
  }
  params.engine_components_factory =
      std::make_unique<EngineComponentsFactoryImpl>(
          EngineSwitchesFromCommandLine());

  params.encryptor = std::move(encryptors[1]);

  if (!IsLocalSyncEnabled()) {
    auth_manager_->ConnectionOpened();

    // Ensures that invalidations are enabled, e.g. when the sync was just
    // enabled or after the engine was stopped with clearing data. Note that
    // invalidations are not supported for local sync.
    sync_client_->GetSyncInvalidationsService()->StartListening();
  }

  engine_->Initialize(std::move(params));
}

void SyncServiceImpl::Shutdown() {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  TRACE_EVENT0("sync", "SyncServiceImpl::Shutdown");

  NotifyShutdown();

  device_statistics_scheduler_.reset();

  // Ensure the LocalDataMigrationItemQueue, the DataTypeManager and the
  // engine are destroyed in order since they hold consecutive pointers to each
  // other.
  std::unique_ptr<SyncEngine> engine =
      ResetEngine(ResetEngineReason::kShutdown);
  local_data_migration_item_queue_.reset();
  data_type_manager_.reset();
  engine.reset();

  crypto_.StopObservingTrustedVaultClient();

  // All observers must be gone now: All KeyedServices should have unregistered
  // their observers already before, in their own Shutdown(), and all others
  // should have done it now when they got the shutdown notification.
  // (Note that destroying the ObserverList triggers its "check_empty" check.)
  observers_.reset();

  auth_manager_.reset();

  identity_manager_observation_.Reset();
}

std::unique_ptr<SyncEngine> SyncServiceImpl::ResetEngine(
    ResetEngineReason reset_reason) {
  TRACE_EVENT0("sync", "SyncServiceImpl::ResetEngine");
  CHECK(data_type_manager_);

  tasks_waiting_for_engine_initialization_.clear();

  const ShutdownReason shutdown_reason =
      ShutdownReasonForResetEngineReason(reset_reason);

  // Stop all data type controllers, if needed. Note that until Stop completes,
  // it is possible in theory to have a ChangeProcessor apply a change from a
  // native model. In that case, it will get applied to the local storage as an
  // unsynced change. That will be persisted, and committed on restart.
  if (shutdown_reason != ShutdownReason::BROWSER_SHUTDOWN_AND_KEEP_DATA) {
    data_type_manager_->Stop(
        ShutdownReasonToSyncStopMetadataFate(shutdown_reason));
    data_type_manager_->SetConfigurer(nullptr);
  }

  if (!engine_) {
    // If the engine hasn't started or is already shut down when a DISABLE_SYNC
    // happens, the Directory needs to be cleaned up here.
    if (shutdown_reason == ShutdownReason::DISABLE_SYNC_AND_CLEAR_DATA) {
      sync_client_->GetSyncEngineFactory()->CleanupOnDisableSync();
    }
    // Depending on the `reset_reason`, maybe clear account-keyed transport
    // data.
    if (ShouldClearTransportDataForAccount(reset_reason)) {
      sync_client_->GetSyncEngineFactory()->ClearTransportDataForAccount(
          signin::GaiaIdHash::FromGaiaId(GetAccountInfo().gaia));
    }
    return nullptr;
  }

  base::UmaHistogramEnumeration("Sync.ResetEngineReason", reset_reason);
  switch (shutdown_reason) {
    case ShutdownReason::STOP_SYNC_AND_KEEP_DATA:
      // Do not stop listening for sync invalidations. Otherwise, GCMDriver
      // would drop all the incoming messages.
      RemoveClientFromServer();
      break;
    case ShutdownReason::DISABLE_SYNC_AND_CLEAR_DATA: {
      sync_client_->GetSyncInvalidationsService()->StopListeningPermanently();
      RemoveClientFromServer();
      break;
    }
    case ShutdownReason::BROWSER_SHUTDOWN_AND_KEEP_DATA:
      sync_client_->GetSyncInvalidationsService()->StopListening();
      break;
  }

  // First, we spin down the engine to stop change processing as soon as
  // possible.
  engine_->StopSyncingForShutdown();

  // Shutdown the migrator before the engine to ensure it doesn't pull a null
  // snapshot.
  migrator_.reset();

  engine_->Shutdown(shutdown_reason);
  std::unique_ptr<SyncEngine> engine_to_be_destroyed = std::move(engine_);

  // Clear various state.
  crypto_.Reset();
  last_snapshot_ = SyncCycleSnapshot();

  // Depending on the `reset_reason`, maybe clear account-keyed transport data.
  if (ShouldClearTransportDataForAccount(reset_reason)) {
    sync_client_->GetSyncEngineFactory()->ClearTransportDataForAccount(
        signin::GaiaIdHash::FromGaiaId(GetAccountInfo().gaia));
  }

  if (!IsLocalSyncEnabled()) {
    auth_manager_->ConnectionClosed();
  }

  DVLOG(2) << "Notify observers on reset engine";
  NotifyObservers();

  // Now that everything is shut down, try to start up again.
  switch (shutdown_reason) {
    case ShutdownReason::STOP_SYNC_AND_KEEP_DATA:
    case ShutdownReason::DISABLE_SYNC_AND_CLEAR_DATA:
      // If Sync is being stopped (either temporarily or permanently),
      // immediately try to start up again. Note that this might start only the
      // transport mode, or it might not start anything at all if something is
      // preventing Sync startup (e.g. the user signed out).
      // Note that TryStart() is guaranteed to *not* have a synchronous effect
      // (it posts a task).
      TryStart();
      break;
    case ShutdownReason::BROWSER_SHUTDOWN_AND_KEEP_DATA:
      // The only exception is browser shutdown: In this case, there's clearly
      // no point in starting up again.
      break;
  }

  return engine_to_be_destroyed;
}

#if BUILDFLAG(IS_ANDROID)
base::android::ScopedJavaLocalRef<jobject> SyncServiceImpl::GetJavaObject() {
  if (!sync_service_android_) {
    sync_service_android_ = std::make_unique<SyncServiceAndroidBridge>(this);
  }
  return sync_service_android_->GetJavaObject();
}
#endif  // BUILDFLAG(IS_ANDROID)

SyncUserSettings* SyncServiceImpl::GetUserSettings() {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  return user_settings_.get();
}

const SyncUserSettings* SyncServiceImpl::GetUserSettings() const {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);
  return user_settings_.get();
}

SyncService::DisableReasonSet SyncServiceImpl::GetDisableReasons() const {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);

  // If Sync is disabled via command line flag, then SyncServiceImpl
  // shouldn't even be instantiated.
  DCHECK(IsSyncAllowedByFlag());
  DisableReasonSet result;

  // If local sync is enabled, most disable reasons don't apply.
  if (!IsLocalSyncEnabled()) {
    if (user_settings_->IsSyncClientDisabledByPolicy() ||
        sync_disabled_by_admin_) {
      result.Put(DISABLE_REASON_ENTERPRISE_POLICY);
    }
    if (!IsSignedIn()) {
      result.Put(DISABLE_REASON_NOT_SIGNED_IN);
    }
  }

  if (unrecoverable_error_reason_) {
    result.Put(DISABLE_REASON_UNRECOVERABLE_ERROR);
  }
  return result;
}

SyncService::TransportState SyncServiceImpl::GetTransportState() const {
  DCHECK_CALLED_ON_VALID_SEQUENCE(sequence_checker_);

  if (!GetDisableReasons().empty()) {
    // Note: we generally shouldn't have an engine while in a disabled state,
    // but it can happen if this method gets called during ResetEngine().
    return TransportState::DISABLED;
  }

  if (auth_manager_->IsSyncPaused()) {
    return TransportState::PAUSED;
  }

  CHECK(IsEngineAllowedToRun());

  if (!engine_) {
    // Starting the engine is allowed but didn't happen. There are three
    // possible scenarios:
    // 1) Startup was deferred, in which case it can take noticeably long until
    //  . the engine initializes. This case can be distinguished by checking if
    //  . `deferring_first_start_since_` is set.
    // 2) Startup is about to happen because SyncServiceImpl::TryStart() was
    //  . invoked, but the posted task to run SyncServiceImpl::TryStartImpl()
    //  . hasn't been processed yet.
    // 3) The service is shutting down.
    //
    // This function reports TransportState::START_DEFERRED only for the first,
    // which is the only real deferred case.
    return deferring_first_start_since_.is_null()
               ? TransportState::INITIALIZING
               : TransportState::START_DEFERRED;
  }

  if (!engine_->IsInitialized() || !data_type_manager_) {
    return TransportState::INITIALIZING;
  }

  if (base::FeatureList::IsEnabled(kSyncDetermineAccountManagedStatus)) {
    // Determining the account's managed-ness status is also considered part of
    // initialization.
    if (!IsLocalSyncEnabled() &&
        auth_manager_->GetActiveAccountInfo().managed_status ==
            signin::AccountManagedStatusFinderOutcome::kPending) {
      return TransportState::INITIALIZING;
    }
  }

  // At this point we should usually be able to configure our data types (so the
  // DataTypeManager should not be STOPPED anymore), unless setup is in
  // progress. But it can also happen if this gets called from DataTypeManager
  // itself.
  if (data_type_manager_->state() == DataTypeManager::STOPPED) {
    return TransportState::PENDING_DESIRED_CONFIGURATION;
  }

  if (data_type_manager_->state() != DataTypeManager::CONFIGURED) {
    return TransportState::CONFIGURING;
  }

  return TransportState::ACTIVE;
}


>>> 
 SyncService::UserActionableError 
 SyncServiceImpl::GetUserActionableError 
 () 
<<< 
...} ...  
```
### patch
```cpp
SyncService::UserActionableError SyncServiceImpl::GetUserActionableError_ChromiumImpl()

```

### match
```cpp
...
 
 namespace syncer { ... 
 
 void SyncServiceImpl::NotifyObservers() { ... 
>>> 
 GetUserActionableError() 
 ; 
<<< 
...} ...  } ...  
```
### patch
```cpp
      GetUserActionableError_ChromiumImpl();

```

