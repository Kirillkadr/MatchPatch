### match
```cpp
...
#include <optional>

 #include <variant>
 
 >>> 
#include "components/content_settings/core/browser/content_settings_utils.h"

 ... 
```
### patch
```cpp
#include "base/containers/fixed_flat_set.h"
#include "components/content_settings/core/browser/content_settings_utils.h"
#include "components/content_settings/core/common/content_settings_types.h"
#include "components/content_settings/core/common/features.h"

```

### match
```cpp
...
 namespace 
 content_settings 
 { 
 >>> 
ContentSettingsInfo::ContentSettingsInfo(
    const PermissionSettingsInfo* permission_settings_info,
    Delegate* delegate,
    const std::set<ContentSetting>& valid_settings,
    IncognitoBehavior incognito_behavior)
    : permission_settings_info_(permission_settings_info),
      delegate_(delegate),
      valid_settings_(valid_settings),
      incognito_behavior_(incognito_behavior) {
  delegate->set_content_settings_info(this);
}
 ... } ...  
```
### patch
```cpp
namespace {
bool IsMorePermissive_BraveImpl(ContentSettingsType content_type,
                                ContentSetting setting,
                                ContentSetting initial_setting) {
  // These types have additional logic for OffTheRecord profiles to always
  // return BLOCK (with a random timeout) instead of inheriting the setting.
  //
  // We must be careful to not break this, otherwise
  // ProcessIncognitoInheritanceBehavior() will return `initial_setting` which
  // is usually ASK and incorrect for OffTheRecord profiles.
  static constexpr auto kOffTheRecordAwareTypes =
      base::MakeFixedFlatSet<ContentSettingsType>({
          ContentSettingsType::NOTIFICATIONS,
          ContentSettingsType::PROTECTED_MEDIA_IDENTIFIER,
          ContentSettingsType::IDLE_DETECTION,
          ContentSettingsType::BRAVE_HTTPS_UPGRADE,
      });

  const bool is_more_permissive = IsMorePermissive(setting, initial_setting);
  if (is_more_permissive || kOffTheRecordAwareTypes.contains(content_type) ||
      base::FeatureList::IsEnabled(kAllowIncognitoPermissionInheritance)) {
    return is_more_permissive;
  }

  // If the type doesn't have special OffTheRecord handling, force
  // ProcessIncognitoInheritanceBehavior() to always return `initial_setting`.
  return true;
}

}  // namespace

```

### match
```cpp
...
 
 namespace content_settings { ... 
 
 PermissionSetting ContentSettingsInfo::Delegate::InheritInIncognito(
    const PermissionSetting& setting) const { ... 
>>> 
 if 
 (IsMorePermissive(content_setting, initial_setting)) 
 { 
<<< 
return initial_setting;
 ... } ...  } ...  } ...  
```
### patch
```cpp
      if (IsMorePermissive_BraveImpl(info_->website_settings_info()->type(),content_setting, initial_setting)) {

```

