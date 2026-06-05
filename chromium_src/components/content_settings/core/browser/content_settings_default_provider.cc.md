### match
```cpp
...
#include <memory>

 #include <string>
 
 >>> 
#include "base/auto_reset.h"

 ... 
```
### patch
```cpp
#include "build/build_config.h"
#include "components/prefs/pref_service.h"
#include "components/prefs/pref_value_map.h"

```

### match
```cpp
...
 
 namespace content_settings { ... 
 
 base::Value DefaultProvider::ReadFromPref(ContentSettingsType content_type) { ... 
 const base::Value& value = prefs_->GetValue(GetPrefName(content_type)); 
 >>> 
// Validate settings.
 ... } ...  } ...  
```
### patch
```cpp
  if (IsBraveValidDefaultValue(content_type, value)) {
    return value.Clone();
  }
  #if !BUILDFLAG(IS_IOS)
  const std::string& autoplay_pref =
      GetPrefName(ContentSettingsType::AUTOPLAY);
  if (IntToContentSetting(prefs_->GetInteger(autoplay_pref)) ==
      ContentSetting::CONTENT_SETTING_ASK) {
    prefs_->ClearPref(autoplay_pref);
  }
#else
const std::string& autoplay_pref =
      GetPrefName(ContentSettingsType::AUTOPLAY);
  if (IntToContentSetting(prefs_->GetInteger(autoplay_pref)) ==
      ContentSetting::CONTENT_SETTING_ASK) {
    prefs_->ClearPref(autoplay_pref);
  }
#endif

```

### match
```cpp
...
 
 namespace content_settings { ... 
void DefaultProvider::RecordHistogramMetrics() {
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultCookiesSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::COOKIES))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultPopupsSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::POPUPS))),
      CONTENT_SETTING_NUM_SETTINGS);

#if BUILDFLAG(USE_BLINK)
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultSubresourceFilterSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::ADS))),
      CONTENT_SETTING_NUM_SETTINGS);
#endif

#if !BUILDFLAG(IS_IOS)
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultImagesSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::IMAGES))),
      CONTENT_SETTING_NUM_SETTINGS);

  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultJavaScriptSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::JAVASCRIPT))),
      CONTENT_SETTING_NUM_SETTINGS);

  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultLocationSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::GEOLOCATION))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultNotificationsSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::NOTIFICATIONS))),
      CONTENT_SETTING_NUM_SETTINGS);

  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultMediaStreamMicSetting",
      IntToContentSetting(prefs_->GetInteger(
          GetPrefName(ContentSettingsType::MEDIASTREAM_MIC))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultMediaStreamCameraSetting",
      IntToContentSetting(prefs_->GetInteger(
          GetPrefName(ContentSettingsType::MEDIASTREAM_CAMERA))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultMIDISysExSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::MIDI_SYSEX))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultWebBluetoothGuardSetting",
      IntToContentSetting(prefs_->GetInteger(
          GetPrefName(ContentSettingsType::BLUETOOTH_GUARD))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultBackgroundSyncSetting",
      IntToContentSetting(prefs_->GetInteger(
          GetPrefName(ContentSettingsType::BACKGROUND_SYNC))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultAutoplaySetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::AUTOPLAY))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultSoundSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::SOUND))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultUsbGuardSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::USB_GUARD))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultIdleDetectionSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::IDLE_DETECTION))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultStorageAccessSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::STORAGE_ACCESS))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultAutoVerifySetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::ANTI_ABUSE))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultJavaScriptOptimizationSetting",
      IntToContentSetting(prefs_->GetInteger(
          GetPrefName(ContentSettingsType::JAVASCRIPT_OPTIMIZER))),
      CONTENT_SETTING_NUM_SETTINGS);
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultSensorsSetting",
      IntToContentSetting(
          prefs_->GetInteger(GetPrefName(ContentSettingsType::SENSORS))),
      CONTENT_SETTING_NUM_SETTINGS);
#endif

#if BUILDFLAG(IS_ANDROID)
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultAutoDarkWebContentSetting",
      IntToContentSetting(prefs_->GetInteger(
          GetPrefName(ContentSettingsType::AUTO_DARK_WEB_CONTENT))),
      CONTENT_SETTING_NUM_SETTINGS);

#endif

#if BUILDFLAG(IS_ANDROID) || BUILDFLAG(IS_IOS)
  base::UmaHistogramEnumeration(
      "ContentSettings.RegularProfile.DefaultRequestDesktopSiteSetting",
      IntToContentSetting(prefs_->GetInteger(
          GetPrefName(ContentSettingsType::REQUEST_DESKTOP_SITE))),
      CONTENT_SETTING_NUM_SETTINGS);

#endif
}
 } 
 // namespace content_settings 
 >>> 
 ... 
```
### patch
```cpp
namespace {

bool IsBraveValidDefaultValue(ContentSettingsType content_type,
                              const base::Value& value) {
  return value.is_dict() &&
         content_settings::IsShieldsContentSettingsType(content_type);
}

}  // namespace
```

