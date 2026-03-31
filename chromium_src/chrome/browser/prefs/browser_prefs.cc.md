### match
```cpp
...
#include <string>

 #include <string_view>
 
 >>> 
#include "base/files/file_path.h"

 ... 
```
### patch
```cpp
#include "base/check.h"

```

### match
```cpp
...
#include "base/time/time.h"

 #include "base/trace_event/trace_event.h"
 
 >>> 
#include "build/android_buildflags.h"

 ... 
```
### patch
```cpp
#include "brave/browser/brave_local_state_prefs.h"
#include "brave/browser/brave_profile_prefs.h"
#include "brave/browser/brave_stats/brave_stats_updater.h"
#include "brave/browser/misc_metrics/uptime_monitor_impl.h"
#include "brave/browser/translate/brave_translate_prefs_migration.h"
#include "brave/components/ai_chat/core/common/buildflags/buildflags.h"
#include "brave/components/brave_adaptive_captcha/prefs_util.h"
#include "brave/components/brave_ads/buildflags/buildflags.h"
#include "brave/components/brave_news/common/buildflags/buildflags.h"
#include "brave/components/brave_rewards/core/buildflags/buildflags.h"
#include "brave/components/brave_search_conversion/p3a.h"
#include "brave/components/brave_shields/content/browser/ad_block_service.h"
#include "brave/components/brave_shields/core/browser/brave_shields_p3a.h"
#include "brave/components/brave_sync/brave_sync_prefs.h"
#include "brave/components/brave_vpn/common/buildflags/buildflags.h"
#include "brave/components/brave_wallet/common/buildflags/buildflags.h"
#include "brave/components/constants/pref_names.h"
#include "brave/components/ipfs/ipfs_prefs.h"
#include "brave/components/l10n/common/prefs.h"
#include "brave/components/ntp_background_images/browser/ntp_background_images_service.h"
#include "brave/components/ntp_background_images/buildflags/buildflags.h"
#include "brave/components/ntp_background_images/common/view_counter_pref_registry.h"
#include "brave/components/omnibox/browser/brave_omnibox_prefs.h"
#include "brave/components/p3a/metric_log_store.h"
#include "brave/components/p3a/rotation_scheduler.h"
#include "brave/components/speedreader/common/buildflags/buildflags.h"
#include "brave/components/tor/buildflags/buildflags.h"

```

### match
```cpp
...
#include "chrome/browser/printing/print_preview_sticky_settings.h"

 #include "chrome/browser/privacy_sandbox/notice/notice_storage.h"
 
 >>> 
#include "chrome/browser/profiles/chrome_version_service.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/profiles/profile.h"

```

### match
```cpp
...
#include "chrome/browser/webauthn/webauthn_pref_names.h"

 #include "chrome/common/buildflags.h"
 
 >>> 
#include "chrome/common/pref_names.h"

 ... 
```
### patch
```cpp
#include "chrome/common/channel_info.h"

```

### match
```cpp
...
#include "components/enterprise/connectors/core/connectors_prefs.h"

 #include "components/feature_engagement/public/pref_names.h"
 
 >>> 
#include "components/history_clusters/core/history_clusters_prefs.h"

 ... 
```
### patch
```cpp
#include "components/gcm_driver/gcm_buildflags.h"

```

### match
```cpp
...
#include "printing/buildflags/buildflags.h"

 #include "rlz/buildflags/buildflags.h"
 
 >>> 
#if BUILDFLAG(ENABLE_BACKGROUND_MODE)
#include "chrome/browser/background/extensions/background_mode_manager.h"
#endif
 ... 
```
### patch
```cpp
#include "third_party/widevine/cdm/buildflags.h"

#if BUILDFLAG(ENABLE_AI_CHAT)
#include "brave/components/ai_chat/core/browser/model_service.h"
#endif

#if BUILDFLAG(ENABLE_BRAVE_ADS)
#include "brave/components/brave_ads/core/public/prefs/obsolete_pref_util.h"
#endif

#if BUILDFLAG(ENABLE_BRAVE_NEWS)
#include "brave/components/brave_news/browser/brave_news_p3a.h"
#include "brave/components/brave_news/common/p3a_pref_names.h"
#include "brave/components/brave_news/common/pref_names.h"
#endif  // BUILDFLAG(ENABLE_BRAVE_NEWS)

#if BUILDFLAG(ENABLE_BRAVE_REWARDS)
#include "brave/browser/brave_rewards/rewards_prefs_util.h"
#endif

#if !BUILDFLAG(IS_ANDROID)
#include "brave/browser/ui/tabs/brave_tab_prefs.h"
#include "brave/browser/ui/webui/welcome_page/brave_welcome_ui_prefs.h"
#endif

#if BUILDFLAG(ENABLE_BRAVE_VPN)
#include "brave/components/brave_vpn/common/brave_vpn_utils.h"
#endif

#if BUILDFLAG(ENABLE_BRAVE_WALLET)
#include "brave/components/brave_wallet/browser/keyring_service.h"
#include "brave/components/brave_wallet/browser/pref_names.h"
#include "brave/components/decentralized_dns/core/utils.h"
#endif

#if BUILDFLAG(ENABLE_TOR)
#include "brave/components/tor/pref_names.h"
#include "brave/components/tor/tor_utils.h"
#endif

#if BUILDFLAG(ENABLE_WIDEVINE)
#include "brave/browser/widevine/widevine_utils.h"
#endif

#if !BUILDFLAG(ENABLE_EXTENSIONS)
#define CHROME_BROWSER_WEB_APPLICATIONS_WEB_APP_PROVIDER_H_
#endif  // !BUILDFLAG(ENABLE_EXTENSIONS)

```

### match
```cpp
...
>>>
 void 
 MigrateObsoleteLocalStatePrefs(PrefService* local_state) 
 {  <<< 
// IMPORTANT NOTE: This code is *not* run on iOS Chrome. If a pref is migrated
 ... } ...  
```
### patch
```cpp
void MigrateObsoleteLocalStatePrefs_ChromiumImpl(PrefService* local_state) {

```

### match
```cpp
...
>>>
 void 
 MigrateObsoleteProfilePrefs 
 ( 
 PrefService* profile_prefs 
 ,  <<< 
const base::FilePath& profile_path
 ... ) ...  
```
### patch
```cpp
void MigrateObsoleteProfilePrefs_ChromiumImpl(PrefService* profile_prefs,

```

### match
```cpp
...
 
 void MigrateObsoleteProfilePrefs_ChromiumImpl(PrefService* profile_prefs,
const base::FilePath& profile_path) { ... 
// Added 09/2025.  >>> 
 PageColorsController::MigrateObsoleteProfilePrefs(profile_prefs);  <<< 
profile_prefs->ClearPref(kGaiaCookieLastListAccountsData);
 ... } ...  
```
### patch
```cpp
  PageColorsController::MigrateObsoleteProfilePrefs_ChromiumImpl(profile_prefs);

```

### match
```cpp
...
 
 void MigrateObsoleteProfilePrefs_ChromiumImpl(PrefService* profile_prefs,
const base::FilePath& profile_path) { ... 

  // IMPORTANT NOTE: This code is *not* run on iOS Chrome. If a pref is migrated
  // or cleared here, and that pref is also used in iOS Chrome, it may also need
  // to be migrated or cleared specifically for iOS as well. This could be by
  // doing the migration in feature code that's called by all platforms instead
  // of here, or by calling migration code in the appropriate place for iOS
  // specifically, e.g. ios/chrome/browser/shared/model/prefs/browser_prefs.mm.

  // BEGIN_MIGRATE_OBSOLETE_PROFILE_PREFS
  // Please don't delete the preceding line. It is used by PRESUBMIT.py.

#if !BUILDFLAG(IS_ANDROID)
  // Added 08/2024, but DO NOT REMOVE after the usual year.
  // TODO(crbug.com/356148174): Remove once kMoveThemePrefsToSpecifics has been
  // enabled for an year.
  MigrateSyncingThemePrefsToNonSyncingIfNeeded(profile_prefs);
#endif  // !BUILDFLAG(IS_ANDROID)

  // Added 10/2025.
  profile_prefs->ClearPref(kSessionRestoreTurnOffFromRestartInfoBarTimesShown);
  profile_prefs->ClearPref(kSessionRestoreTurnOffFromSessionInfoBarTimesShown);
  profile_prefs->ClearPref(kSessionRestorePrefChanged);

  // Added 05/2025.
  profile_prefs->ClearPref(kPrivacySandboxFakeNoticePromptShownTimeSync);
  profile_prefs->ClearPref(kPrivacySandboxFakeNoticePromptShownTime);
  profile_prefs->ClearPref(kPrivacySandboxFakeNoticeFirstSignInTime);
  profile_prefs->ClearPref(kPrivacySandboxFakeNoticeFirstSignOutTime);

  privacy_sandbox::PrivacySandboxNoticeStorage::UpdateNoticeSchemaV2(
      profile_prefs);

  // Check MigrateDeprecatedAutofillPrefs() to see if this is safe to remove.
  autofill::prefs::MigrateDeprecatedAutofillPrefs(profile_prefs);

  // TODO(326079444): After experiment is over, update the deprecated date and
  // allow this to be cleaned up.
#if !BUILDFLAG(IS_ANDROID) && !BUILDFLAG(IS_CHROMEOS)
  MigrateDefaultBrowserLastDeclinedPref(profile_prefs);
#endif

  // Added 04/2025.
  profile_prefs->ClearPref(kDefaultSearchProviderChoiceScreenShuffleMilestone);

  // Added 04/2025.
  profile_prefs->ClearPref(kAddedBookmarkSincePowerBookmarksLaunch);

  // Added 04/2025.
  profile_prefs->ClearPref(kGlicRolloutEligibility);

  // Added 04/2025
  profile_prefs->ClearPref(kManagedAccessToGetAllScreensMediaAllowedForUrls);

#if BUILDFLAG(IS_ANDROID)
  // Added 04/2025
  profile_prefs->ClearPref(
      kObsoleteUserAcknowledgedLocalPasswordsMigrationWarning);

  // Added 04/2025.
  profile_prefs->ClearPref(kObsoleteLocalPasswordMigrationWarningPrefsVersion);
#endif

  // Added 04/2025.
  profile_prefs->ClearPref(kSuggestionGroupVisibility);

#if BUILDFLAG(IS_ANDROID)
  // Added 05/2025.
  profile_prefs->ClearPref(kWipedWebAPkDataForMigration);
#endif  // BUILDFLAG(IS_ANDROID)

  // Added 05/2025.
  profile_prefs->ClearPref(kSyncCacheGuid);
  profile_prefs->ClearPref(kSyncBirthday);
  profile_prefs->ClearPref(kSyncBagOfChips);
  profile_prefs->ClearPref(kSyncLastSyncedTime);
  profile_prefs->ClearPref(kSyncLastPollTime);
  profile_prefs->ClearPref(kSyncPollInterval);
  profile_prefs->ClearPref(kSharingVapidKey);
  profile_prefs->ClearPref(kHasSeenWelcomePage);

  // Added 06/2025.
  profile_prefs->ClearPref(kStorageGarbageCollect);
  profile_prefs->ClearPref(kGaiaCookiePeriodicReportTimeDeprecated);
  profile_prefs->ClearPref(kWebAuthnCablePairingsPrefName);
  profile_prefs->ClearPref(kLastUsedPairingFromSyncPublicKey);
  profile_prefs->ClearPref(kSyncedDefaultSearchProviderGUID);

#if BUILDFLAG(IS_ANDROID)
  // Deprecated 07/2025.
  profile_prefs->ClearPref(
      kObsoletePasswordAccessLossWarningShownAtStartupTimestamp);
  profile_prefs->ClearPref(kObsoletePasswordAccessLossWarningShownTimestamp);
  profile_prefs->ClearPref(kObsoleteTimeOfLastMigrationAttempt);
  profile_prefs->ClearPref(kObsoleteSettingsMigratedToUPMLocal);
  profile_prefs->ClearPref(
      kObsoleteShouldShowPostPasswordMigrationSheetAtStartup);
  profile_prefs->ClearPref(
      kObsoleteUnenrolledFromGoogleMobileServicesDueToErrors);
  profile_prefs->ClearPref(
      kObsoleteCurrentMigrationVersionToGoogleMobileServices);
#endif  // BUILDFLAG(IS_ANDROID)

  // Added 07/2025.
  profile_prefs->ClearPref(kFirstSyncCompletedInFullSyncMode);
  profile_prefs->ClearPref(kGoogleServicesSecondLastSyncingGaiaId);

#if BUILDFLAG(IS_CHROMEOS)
  // Added 07/2025.
  profile_prefs->ClearPref(kAssistantNumSessionsWhereOnboardingShown);
  profile_prefs->ClearPref(kAssistantTimeOfLastInteraction);

  // Added 07/2025.
  profile_prefs->ClearPref(kAssistantConsentStatus);
  profile_prefs->ClearPref(kAssistantContextEnabled);
  profile_prefs->ClearPref(kAssistantDisabledByPolicy);
  profile_prefs->ClearPref(kAssistantEnabled);
  profile_prefs->ClearPref(kAssistantHotwordAlwaysOn);
  profile_prefs->ClearPref(kAssistantHotwordEnabled);
  profile_prefs->ClearPref(kAssistantLaunchWithMicOpen);
  profile_prefs->ClearPref(kAssistantNotificationEnabled);
  profile_prefs->ClearPref(kAssistantVoiceMatchEnabledDuringOobe);
  profile_prefs->ClearPref(kAssistantOnboardingMode);
  profile_prefs->ClearPref(kAssistantNumFailuresSinceLastServiceRun);
#endif

  // Added 07/2025
  profile_prefs->ClearPref(kOptGuideModelFetcherLastFetchAttempt);
  profile_prefs->ClearPref(kOptGuideModelFetcherLastFetchSuccess);

#if BUILDFLAG(IS_CHROMEOS)
  // Added 07/2025.
  profile_prefs->ClearPref(kTimeOfFirstFilesAppChipPress);
#endif  // BUILDFLAG(IS_CHROMEOS)

  profile_prefs->ClearPref(kSyncPromoIdentityPillShownCount);
  profile_prefs->ClearPref(kSyncPromoIdentityPillUsedCount);

  // Added 08/2025.
  profile_prefs->ClearPref(kInvalidationClientIDCache);
  profile_prefs->ClearPref(kInvalidationTopicsToHandler);

#if BUILDFLAG(IS_ANDROID)
  // Added 08/2025.
  profile_prefs->ClearPref(kObsoleteAccountStorageNoticeShown);
#endif  // BUILDFLAG(IS_ANDROID)

#if !BUILDFLAG(IS_ANDROID)
  // Deprecated 08/2025.
  profile_prefs->ClearPref(
      kObsoleteAutofillableCredentialsProfileStoreLoginDatabase);
  profile_prefs->ClearPref(
      kObsoleteAutofillableCredentialsAccountStoreLoginDatabase);
#endif  // !BUILDFLAG(IS_ANDROID)

#if !BUILDFLAG(IS_ANDROID)
  // Added 08/2025.
  NewTabPageUI::MigrateDeprecatedUseMostVisitedTilesPref(profile_prefs);
#endif  // !BUILDFLAG(IS_ANDROID)

#if BUILDFLAG(IS_CHROMEOS)
  // Added 08/2025.
  profile_prefs->ClearPref(kDesksLacrosProfileIdList);
#endif  // BUILDFLAG(IS_CHROMEOS)

#if BUILDFLAG(IS_ANDROID)
  // Added 09/2025.
  profile_prefs->ClearPref(kObsoleteUpmUnmigratedPasswordsExported);
  profile_prefs->ClearPref(kObsoletePasswordsUseUPMLocalAndSeparateStores);
  profile_prefs->ClearPref(kObsoleteEmptyProfileStoreLoginDatabase);
  profile_prefs->ClearPref(kObsoleteUpmAutoExportCsvNeedsDeletion);
  base::DeleteFile(profile_path.Append(FILE_PATH_LITERAL("Login Data")));
  base::DeleteFile(
      profile_path.Append(FILE_PATH_LITERAL("Login Data For Account")));
  base::DeleteFile(
      profile_path.Append(FILE_PATH_LITERAL("Login Data-journal")));
  base::DeleteFile(
      profile_path.Append(FILE_PATH_LITERAL("Login Data For Account-journal")));
#endif  // BUILDFLAG(IS_ANDROID)

  // Added 09/2025.
    PageColorsController::MigrateObsoleteProfilePrefs_ChromiumImpl(profile_prefs);
	profile_prefs->ClearPref(kGaiaCookieLastListAccountsData);

  // Added 09/2025.
  profile_prefs->ClearPref(kLensOverlayEduActionChipShownCount);

  SigninPrefs(*profile_prefs).MigrateObsoleteSigninPrefs();

#if !BUILDFLAG(IS_ANDROID)
  // Added 10/2025
  NewTabPageUI::MigrateDeprecatedShortcutsTypePref(profile_prefs);
#endif  // !BUILDFLAG(IS_ANDROID)

  // Added 10/2025.
  profile_prefs->ClearPref(kLegacySyncSessionsGUID);

  // Added 11/2025.
  profile_prefs->ClearPref(kRefreshHeuristicBreakageException);

  // Added 12/2025.
  profile_prefs->ClearPref(kReduceUserAgentMinorVersion);
  profile_prefs->ClearPref(kMerchantTrustUiLastInteractionTime);
  profile_prefs->ClearPref(kMerchantTrustPageInfoLastOpenTime);

  // Added 12/2025.
  profile_prefs->ClearPref(kCloudPrintProxyEnabled);
  profile_prefs->ClearPref(kCloudPrintEmail);

#if BUILDFLAG(IS_ANDROID)
  // Added 01/2026.
  profile_prefs->ClearPref(kDSEGeolocationSettingDeprecated);
  profile_prefs->ClearPref(kDSEPermissionsSettings);
  profile_prefs->ClearPref(kDSEWasDisabledByPolicy);
#endif  // BUILDFLAG(IS_ANDROID)

  // Added 01/2026.
  profile_prefs->ClearPref(kCookieClearOnExitMigrationNoticeComplete);

  // Added 02/2026.
  profile_prefs->ClearPref(kGlicGuestUrlPresetAutopush);
  profile_prefs->ClearPref(kGlicGuestUrlPresetPreprod);
  profile_prefs->ClearPref(kGlicGuestUrlPresetProd);

  // Added 02/2026.
  profile_prefs->ClearPref(kExplicitBrowserSigninWithoutFeatureEnabled);

  // Added 02/2026.
  profile_prefs->ClearPref(kTabSearchOpened);

  // Added 03/2026.
  profile_prefs->ClearPref(kTabDeclutterUsageCount);

  // Added 03/2026.
  profile_prefs->ClearPref(kTabSearchTabIndex);

#if !BUILDFLAG(IS_ANDROID)
  // Added 02/2026.
  tabs::MigrateTabSearchPref(profile_prefs);
#endif  // !BUILDFLAG(IS_ANDROID)

  // Added 03/2026
  profile_prefs->ClearPref(
      kSigninFromBookmarksBubbleSyntheticTrialGroupNamePref);
  profile_prefs->ClearPref(
      kBookmarksBubblePromoShownSyntheticTrialGroupNamePref);

  // Added 03/2026.
  profile_prefs->ClearPref(kSafeBrowsingModuleShownCount);
  profile_prefs->ClearPref(kSafeBrowsingModuleLastCooldownStartAt);
  profile_prefs->ClearPref(kSafeBrowsingModuleOpened);

#if BUILDFLAG(IS_ANDROID)
  // Added 03/2026.
  profile_prefs->ClearPref(kPrivacySandboxActivityTypeRecord2);
#endif  // BUILDFLAG(IS_ANDROID)

  // Added 03/2026.
  profile_prefs->ClearPref(kTabOrganizationNudgeBackoffCount);
  profile_prefs->ClearPref(kTabOrganizationShowFRE);
  profile_prefs->ClearPref(kTabOrganizationModelStrategy);

  // Added 03/2026.
  profile_prefs->ClearPref(kNtpContextMenuClickCount);

  // Added 03/2026.
  privacy_sandbox::ClearAdPrivacyPrefs(profile_prefs);

  // Added 03/2026.
  profile_prefs->ClearPref(kNtpPromoPrefLastSnoozed);

  // Please don't delete the following line. It is used by PRESUBMIT.py.
  // END_MIGRATE_OBSOLETE_PROFILE_PREFS

  // IMPORTANT NOTE: This code is *not* run on iOS Chrome. If a pref is migrated
  // or cleared here, and that pref is also used in iOS Chrome, it may also need
  // to be migrated or cleared specifically for iOS as well. This could be by
  // doing the migration in feature code that's called by all platforms instead
  // of here, or by calling migration code in the appropriate place for iOS
  
 // specifically, e.g. ios/chrome/browser/shared/model/prefs/browser_prefs.mm. 
 >>> 
 ... } ...  
```
### patch
```cpp

  #if !BUILDFLAG(USE_GCM_FROM_PLATFORM)
#include "brave/browser/gcm_driver/brave_gcm_utils.h"
#endif

#if BUILDFLAG(ENABLE_CUSTOM_BACKGROUND)
#include "brave/browser/ntp_background/ntp_background_prefs.h"
#endif

#if defined(TOOLKIT_VIEWS)
#include "brave/components/sidebar/browser/pref_names.h"
#endif

#if BUILDFLAG(ENABLE_SPEEDREADER)
#include "brave/components/speedreader/speedreader_pref_migration.h"
#endif

// This method should be periodically pruned of year+ old migrations.
void MigrateObsoleteProfilePrefs(PrefService* profile_prefs,
                                 const base::FilePath& profile_path) {
  DCHECK(profile_prefs);
  // BEGIN_MIGRATE_OBSOLETE_PROFILE_PREFS
#if !BUILDFLAG(USE_GCM_FROM_PLATFORM)
  // Added 02/2020.
  // Must be called before ChromiumImpl because it's migrating a Chromium pref
  // to Brave pref.
  gcm::MigrateGCMPrefs(profile_prefs);
#endif

#if !BUILDFLAG(IS_ANDROID)
  // Added 06/2025.
  // Must be called before ChromiumImpl because it's migrating a Chromium pref
  // to Brave pref.
  brave::welcome_ui::prefs::MigratePrefs(profile_prefs);
#endif  // !BUILDFLAG(IS_ANDROID)

  MigrateObsoleteProfilePrefs_ChromiumImpl(profile_prefs, profile_path);

  brave_sync::MigrateBraveSyncPrefs(profile_prefs);

#if !BUILDFLAG(IS_ANDROID)
  // Added 10/2022
  profile_prefs->ClearPref(kDefaultBrowserLaunchingCount);
#endif

#if BUILDFLAG(ENABLE_EXTENSIONS)
  // Added 11/2022
  profile_prefs->ClearPref(kDontAskEnableWebDiscovery);
  profile_prefs->ClearPref(kBraveSearchVisitCount);
#endif

#if BUILDFLAG(ENABLE_BRAVE_WALLET)
  brave_wallet::MigrateObsoleteProfilePrefs(profile_prefs);
#endif

#if BUILDFLAG(ENABLE_BRAVE_NEWS)
  // Added 05/2021
  profile_prefs->ClearPref(brave_news::prefs::kBraveNewsIntroDismissed);
#endif
  // Added 07/2021
  profile_prefs->ClearPref(prefs::kNetworkPredictionOptions);

#if BUILDFLAG(ENABLE_BRAVE_REWARDS)
  // Added 01/2022
  brave_rewards::MigrateObsoleteProfilePrefs(profile_prefs);
#endif

  // Added 05/2022
  translate::ClearMigrationBraveProfilePrefs(profile_prefs);

  // Added 06/2022
#if BUILDFLAG(ENABLE_CUSTOM_BACKGROUND)
  NTPBackgroundPrefs(profile_prefs).MigrateOldPref();
#endif

  // Added 24/11/2022: https://github.com/brave/brave-core/pull/16027
#if !BUILDFLAG(IS_IOS) && !BUILDFLAG(IS_ANDROID)
  profile_prefs->ClearPref(kFTXAccessToken);
  profile_prefs->ClearPref(kFTXOauthHost);
  profile_prefs->ClearPref(kFTXNewTabPageShowFTX);
  profile_prefs->ClearPref(kCryptoDotComNewTabPageShowCryptoDotCom);
  profile_prefs->ClearPref(kCryptoDotComHasBoughtCrypto);
  profile_prefs->ClearPref(kCryptoDotComHasInteracted);
  profile_prefs->ClearPref(kGeminiAccessToken);
  profile_prefs->ClearPref(kGeminiRefreshToken);
  profile_prefs->ClearPref(kNewTabPageShowGemini);
#endif

  // Added 24/11/2022: https://github.com/brave/brave-core/pull/16027
#if !BUILDFLAG(IS_IOS)
  profile_prefs->ClearPref(kBinanceAccessToken);
  profile_prefs->ClearPref(kBinanceRefreshToken);
  profile_prefs->ClearPref(kNewTabPageShowBinance);
  profile_prefs->ClearPref(kBraveSuggestedSiteSuggestionsEnabled);
#endif

  // Added 03/2024
#if BUILDFLAG(ENABLE_TOR)
  profile_prefs->ClearPref(tor::prefs::kAutoOnionRedirect);
#endif

#if defined(TOOLKIT_VIEWS)
  // Added May 2023
  if (profile_prefs->GetBoolean(sidebar::kSidebarAlignmentChangedTemporarily)) {
    // If temporarily changed, it means sidebar is set to right.
    // Just clear alignment prefs as default alignment is changed to right.
    profile_prefs->ClearPref(prefs::kSidePanelHorizontalAlignment);
  }

  profile_prefs->ClearPref(sidebar::kSidebarAlignmentChangedTemporarily);
#endif

#if BUILDFLAG(ENABLE_BRAVE_NEWS)
  brave_news::p3a::prefs::MigrateObsoleteProfileNewsMetricsPrefs(profile_prefs);
#endif

  // Added 2023-09
  ntp_background_images::MigrateObsoleteProfilePrefs(profile_prefs);

#if BUILDFLAG(ENABLE_BRAVE_ADS)
  // Added 2023-11
  brave_ads::MigrateObsoleteProfilePrefs(profile_prefs);
#endif

  brave_shields::MigrateObsoleteProfilePrefs(profile_prefs);

#if !BUILDFLAG(IS_ANDROID)
  // Added 2024-01
  brave_tabs::MigrateBraveProfilePrefs(profile_prefs);
#endif  // !BUILDFLAG(IS_ANDROID)

  // Added 2024-04
#if BUILDFLAG(ENABLE_AI_CHAT)
  ai_chat::ModelService::MigrateProfilePrefs(profile_prefs);
#endif

  // Added 2024-05
  ipfs::ClearDeprecatedIpfsPrefs(profile_prefs);

  // Added 2024-07
  profile_prefs->ClearPref(kHangoutsEnabled);

  // Added 2024-10
  brave_adaptive_captcha::MigrateObsoleteProfilePrefs(profile_prefs);

#if BUILDFLAG(IS_ANDROID)
  // Added 27/11/2024: https://github.com/brave/brave-core/pull/26719
  profile_prefs->ClearPref(kSafetynetCheckFailed);
  profile_prefs->ClearPref(kSafetynetStatus);
#endif  // BUILDFLAG(IS_ANDROID)

  // Added 2025-05
#if !BUILDFLAG(IS_IOS) && !BUILDFLAG(IS_ANDROID)
  profile_prefs->ClearPref(kWebTorrentEnabled);
#endif

  // Added 2025-08 - Speedreader preference migration
#if BUILDFLAG(ENABLE_SPEEDREADER)
  speedreader::MigrateObsoleteProfilePrefs(profile_prefs);
#endif

  // END_MIGRATE_OBSOLETE_PROFILE_PREFS
}

// This method should be periodically pruned of year+ old migrations.
void MigrateObsoleteLocalStatePrefs(PrefService* local_state) {
  // BEGIN_MIGRATE_OBSOLETE_LOCAL_STATE_PREFS
  MigrateObsoleteLocalStatePrefs_ChromiumImpl(local_state);

#if BUILDFLAG(ENABLE_TOR)
  // Added 4/2021.
  tor::MigrateLastUsedProfileFromLocalStatePrefs(local_state);
#endif

#if BUILDFLAG(ENABLE_BRAVE_WALLET)
  decentralized_dns::MigrateObsoleteLocalStatePrefs(local_state);
#endif

#if !BUILDFLAG(IS_ANDROID)
  // Added 10/2022
  local_state->ClearPref(kDefaultBrowserPromptEnabled);
#endif

#if BUILDFLAG(ENABLE_BRAVE_VPN)
  // Added 09/2024
  brave_vpn::MigrateLocalStatePrefs(local_state);
#endif

  misc_metrics::UptimeMonitorImpl::MigrateObsoletePrefs(local_state);
  brave_search_conversion::p3a::MigrateObsoleteLocalStatePrefs(local_state);
  brave_shields::MigrateObsoletePrefsForAdBlockService(local_state);
  brave_stats::MigrateObsoleteLocalStatePrefs(local_state);
  brave_l10n::MigrateObsoleteLocalStatePrefs(local_state);
  p3a::MetricLogStore::MigrateObsoleteLocalStatePrefs(local_state);
  p3a::RotationScheduler::MigrateObsoleteLocalStatePrefs(local_state);
#if BUILDFLAG(ENABLE_BRAVE_ADS)
  brave_ads::MigrateObsoleteLocalStatePrefs(local_state);
#endif
  ntp_background_images::NTPBackgroundImagesService::
      MigrateObsoleteLocalStatePrefs(local_state);

  // END_MIGRATE_OBSOLETE_LOCAL_STATE_PREFS
}

#if !BUILDFLAG(ENABLE_EXTENSIONS)
#undef CHROME_BROWSER_WEB_APPLICATIONS_WEB_APP_PROVIDER_H_
#endif  // !BUILDFLAG(ENABLE_EXTENSIONS)

```

