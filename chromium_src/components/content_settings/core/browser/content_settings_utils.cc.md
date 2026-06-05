### match
```cpp
...
#include <array>

 #include <vector>
 
 >>> 
#include "base/notreached.h"

 ... 
```
### patch
```cpp
#include <iostream>
#include "base/check.h"

```

### match
```cpp
...
>>>
 void 
 GetRendererContentSettingRules 
 ( 
 const HostContentSettingsMap* map 
 , 
<<< 
RendererContentSettingRules* rules
 ... ) ...  
```
### patch
```cpp
void GetRendererContentSettingRules_ChromiumImpl(const HostContentSettingsMap* map,

```

### match
```cpp
...
bool CanBeAutoRevokedAsUnusedPermission(ContentSettingsType type,
                                        const base::Value& value,
                                        bool is_one_time) {
  DCHECK(WebsiteSettingsRegistry::GetInstance()->Get(type)) << type;

  // The Permissions module in Safety check will revoke permissions after
  // a finite amount of time.
  // We're only interested in expiring permissions that are either
  // A. permission settings (= PermissionSettingsRegistry-based), which
  //    1. Are ALLOWed.
  //    2. Are of eligible ContentSettingsType.
  //      (That includes the default value being ASK. By definition, all
  //      Permissions are ASK by default. If that changes in the future,
  //      consider whether revocation for such permission makes sense. If not,
  //      make sure last_visited is not unnecessarily tracked for them.)
  //    3. Are not already a one-time grant.
  // B. chooser permissions (= WebsiteSettingsRegistry-based), which
  //    1. Are allowlisted.
  //    2. Have a non-empty value.
  if (is_one_time) {
    return false;
  }

  auto* permission_settings_info =
      PermissionSettingsRegistry::GetInstance()->Get(type);
  if (permission_settings_info) {
    auto setting = permission_settings_info->delegate().FromValue(value);
    // If the setting is already DEFAULT or the value is corrupt, no need to
    // revoke the permission.
    if (!setting.has_value()) {
      return false;
    }

    return permission_settings_info->delegate().IsAnyPermissionAllowed(
               setting.value()) &&
           CanTrackLastVisit(type);
  } else {
    return false;
  }
}
>>> 
 const 
 std::vector<ContentSettingsType> 
 & GetTypesWithTemporaryGrants() 
 { 
<<< 
...} ...  
```
### patch
```cpp
const std::vector<ContentSettingsType>& GetTypesWithTemporaryGrants_ChromiumImpl() {

```

### match
```cpp
...
}
>>> 
 const 
 std::vector<ContentSettingsType> 
 & GetTypesWithTemporaryGrantsInHcsm() 
 { 
<<< 
...} ...  
```
### patch
```cpp
const std::vector<ContentSettingsType>& GetTypesWithTemporaryGrantsInHcsm_ChromiumImpl() {

```

### match
```cpp
...
 
 bool ShouldTypeExpireActively(ContentSettingsType type) { ... 
>>> 
 std::ranges::contains(GetTypesWithTemporaryGrantsInHcsm(), type) 
 ; 
<<< 
...} ...  
```
### patch
```cpp
         std::ranges::contains(GetTypesWithTemporaryGrantsInHcsm_ChromiumImpl(), type);

```

### match
```cpp
...
 
 base::Value PermissionSettingToValue(const PermissionSettingsInfo* info,
                                     const PermissionSetting& setting) { ... 
return value;
 } 
 >>> 
 ... 
```
### patch
```cpp
void GetRendererContentSettingRules(const HostContentSettingsMap* map,
                                    RendererContentSettingRules* rules) {
  GetRendererContentSettingRules_ChromiumImpl(map, rules);
  std::pair<ContentSettingsType, ContentSettingsForOneType*> settings[] = {
      {ContentSettingsType::AUTOPLAY, &rules->autoplay_rules},
      {ContentSettingsType::BRAVE_FINGERPRINTING_V2,
       &rules->fingerprinting_rules},
      {ContentSettingsType::BRAVE_SHIELDS, &rules->brave_shields_rules},
      {ContentSettingsType::BRAVE_COSMETIC_FILTERING,
       &rules->cosmetic_filtering_rules},
  };
  for (const auto& setting : settings) {
    DCHECK(
        RendererContentSettingRules::IsRendererContentSetting(setting.first));
    *setting.second = map->GetSettingsForOneType(setting.first);
  }
  for (auto webcompat_settings_type = ContentSettingsType::BRAVE_WEBCOMPAT_NONE;
       webcompat_settings_type != ContentSettingsType::BRAVE_WEBCOMPAT_ALL;
       webcompat_settings_type = static_cast<ContentSettingsType>(
           static_cast<int32_t>(webcompat_settings_type) + 1)) {
    rules->webcompat_rules[webcompat_settings_type] =
        map->GetSettingsForOneType(webcompat_settings_type);
  }
}
const std::vector<ContentSettingsType>& GetTypesWithTemporaryGrants() {
  static base::NoDestructor<const std::vector<ContentSettingsType>> types;
  return *types;
}

const std::vector<ContentSettingsType>& GetTypesWithTemporaryGrantsInHcsm() {
  static base::NoDestructor<const std::vector<ContentSettingsType>> types;
  return *types;
}

```

