### match
```cpp
...
#include <variant>

 #include <vector>
 
 >>> 
#include "base/check_op.h"

 ... 
```
### patch
```cpp
#include <vector>
#include "base/check.h"

```

### match
```cpp
...
>>>
 bool 
 RendererContentSettingRules::IsRendererContentSetting 
 (  <<< 
ContentSettingsType content_type
 ... ) ...  
```
### patch
```cpp
bool RendererContentSettingRules_ChromiumImpl::IsRendererContentSetting(

```

### match
```cpp
...
>>>
 void 
 RendererContentSettingRules::FilterRulesByOutermostMainFrameURL 
 (  <<< 
const GURL& outermost_main_frame_url
 ... ) ...  
```
### patch
```cpp
void RendererContentSettingRules_ChromiumImpl::FilterRulesByOutermostMainFrameURL(

```

### match
```cpp
...
void RendererContentSettingRules_ChromiumImpl::FilterRulesByOutermostMainFrameURL(
const GURL& outermost_main_frame_url) {
  FilterRulesForType(mixed_content_rules, outermost_main_frame_url);
}  >>> 
 RendererContentSettingRules::RendererContentSettingRules() = default;  <<< 
RendererContentSettingRules::~RendererContentSettingRules() = default;
 ... 
```
### patch
```cpp
RendererContentSettingRules_ChromiumImpl::RendererContentSettingRules_ChromiumImpl() = default;

```

### match
```cpp
...
RendererContentSettingRules_ChromiumImpl::RendererContentSettingRules_ChromiumImpl() = default;  >>> 
 RendererContentSettingRules::~RendererContentSettingRules() = default; 
 RendererContentSettingRules::RendererContentSettingRules(
    const RendererContentSettingRules&) = default;  <<< 
RendererContentSettingRules::RendererContentSettingRules(
    RendererContentSettingRules&& rules) = default;
 ... 
```
### patch
```cpp
RendererContentSettingRules_ChromiumImpl::~RendererContentSettingRules_ChromiumImpl() = default;

```

### match
```cpp
...
RendererContentSettingRules_ChromiumImpl::~RendererContentSettingRules_ChromiumImpl() = default;  >>> 
 RendererContentSettingRules::RendererContentSettingRules(
    RendererContentSettingRules&& rules) = default; 
 RendererContentSettingRules& RendererContentSettingRules::operator=(
    const RendererContentSettingRules& rules) = default;  <<< 
RendererContentSettingRules& RendererContentSettingRules::operator=(
    RendererContentSettingRules&& rules) = default;
 ... 
```
### patch
```cpp
RendererContentSettingRules_ChromiumImpl::RendererContentSettingRules_ChromiumImpl(
    const RendererContentSettingRules_ChromiumImpl&) = default;

```

### match
```cpp
...
RendererContentSettingRules_ChromiumImpl::RendererContentSettingRules_ChromiumImpl(
    const RendererContentSettingRules_ChromiumImpl&) = default;  >>> 
 RendererContentSettingRules& RendererContentSettingRules::operator=(
    RendererContentSettingRules&& rules) = default; 
 bool RendererContentSettingRules::operator==(
    const RendererContentSettingRules& other) const = default;  <<< 
content_settings::SettingInfo::SettingInfo() = default;
 ... 
```
### patch
```cpp
RendererContentSettingRules_ChromiumImpl::RendererContentSettingRules_ChromiumImpl(
    RendererContentSettingRules_ChromiumImpl&& rules) = default;

RendererContentSettingRules_ChromiumImpl& RendererContentSettingRules_ChromiumImpl::operator=(
    const RendererContentSettingRules_ChromiumImpl& rules) = default;

RendererContentSettingRules_ChromiumImpl& RendererContentSettingRules_ChromiumImpl::operator=(
    RendererContentSettingRules_ChromiumImpl&& rules) = default;

bool RendererContentSettingRules_ChromiumImpl::operator==(
    const RendererContentSettingRules_ChromiumImpl& other) const = default;

```

### match
```cpp
...
 
 std::ostream& operator<<(std::ostream& os,
                         const std::optional<PermissionSetting>& it) { ... 
return os << *it;
 } 
 >>> 
 ... 
```
### patch
```cpp
RendererContentSettingRules::RendererContentSettingRules() = default;
RendererContentSettingRules::~RendererContentSettingRules() = default;

RendererContentSettingRules::RendererContentSettingRules(
    const RendererContentSettingRules&) = default;

RendererContentSettingRules::RendererContentSettingRules(
    RendererContentSettingRules&& rules) = default;

RendererContentSettingRules& RendererContentSettingRules::operator=(
    const RendererContentSettingRules& rules) = default;

RendererContentSettingRules& RendererContentSettingRules::operator=(
    RendererContentSettingRules&& rules) = default;

// static
bool RendererContentSettingRules::IsRendererContentSetting(
    ContentSettingsType content_type) {
  return RendererContentSettingRules_ChromiumImpl::IsRendererContentSetting(
             content_type) ||
         content_type == ContentSettingsType::AUTOPLAY ||
         content_type == ContentSettingsType::BRAVE_COSMETIC_FILTERING ||
         content_type == ContentSettingsType::BRAVE_FINGERPRINTING_V2 ||
         content_type == ContentSettingsType::BRAVE_GOOGLE_SIGN_IN ||
         content_type == ContentSettingsType::BRAVE_SHIELDS;
}

void RendererContentSettingRules::FilterRulesByOutermostMainFrameURL(
    const GURL& outermost_main_frame_url) {
  RendererContentSettingRules_ChromiumImpl::FilterRulesByOutermostMainFrameURL(
      outermost_main_frame_url);
  FilterRulesForType(autoplay_rules, outermost_main_frame_url);
  FilterRulesForType(brave_shields_rules, outermost_main_frame_url);
  // FilterRulesForType has a DCHECK on the size and these fail (for now)
  // because they incorrectly use CONTENT_SETTINGS_DEFAULT as a distinct setting
  std::erase_if(
      cosmetic_filtering_rules,
      [&outermost_main_frame_url](const ContentSettingPatternSource& source) {
        return !source.primary_pattern.Matches(outermost_main_frame_url);
      });
  std::erase_if(
      fingerprinting_rules,
      [&outermost_main_frame_url](const ContentSettingPatternSource& source) {
        return !source.primary_pattern.Matches(outermost_main_frame_url);
      });
}
namespace content_settings {
namespace {

bool IsExplicitSetting(const ContentSettingsPattern& primary_pattern,
                       const ContentSettingsPattern& secondary_pattern) {
  return !primary_pattern.MatchesAllHosts() ||
         !secondary_pattern.MatchesAllHosts();
}

}  // namespace

bool IsExplicitSetting(const ContentSettingPatternSource& setting) {
  return IsExplicitSetting(setting.primary_pattern, setting.secondary_pattern);
}

bool IsExplicitSetting(const SettingInfo& setting) {
  return IsExplicitSetting(setting.primary_pattern, setting.secondary_pattern);
}

}  // namespace content_settings
```

