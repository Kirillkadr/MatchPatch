### match
```cpp
...
 
 # ifndef ... 
#define COMPONENTS_CONTENT_SETTINGS_CORE_COMMON_CONTENT_SETTINGS_MOJOM_TRAITS_H_

 #include <string>
 
 >>> 
#include "base/values.h"

 ...
```
### patch
```cpp
#include "components/content_settings/core/common/content_settings.h"
#include "components/content_settings/core/common/content_settings.mojom.h"

```

### match
```cpp
... >>> 
 template <>
struct StructTraits<
    content_settings::mojom::RendererContentSettingRulesDataView,
    RendererContentSettingRules> {
  static const std::vector<ContentSettingPatternSource>& mixed_content_rules(
      const RendererContentSettingRules& r) {
    return r.mixed_content_rules;
  }

  static bool Read(
      content_settings::mojom::RendererContentSettingRulesDataView data,
      RendererContentSettingRules* out);
};
   <<<    ...
```
### patch
```cpp
    template <>
struct StructTraits<
    content_settings::mojom::RendererContentSettingRulesDataView,
    RendererContentSettingRules_ChromiumImpl> {
  static const std::vector<ContentSettingPatternSource>& mixed_content_rules(
      const RendererContentSettingRules_ChromiumImpl& r) {
    return r.mixed_content_rules;
  }

  static bool Read(
      content_settings::mojom::RendererContentSettingRulesDataView data,
      RendererContentSettingRules_ChromiumImpl* out);
};

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace mojo { ... 
 
 struct StructTraits<
    content_settings::mojom::RendererContentSettingRulesDataView,
    RendererContentSettingRules_ChromiumImpl> { ... 
static bool Read(
      content_settings::mojom::RendererContentSettingRulesDataView data,
      RendererContentSettingRules_ChromiumImpl* out);
 } 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
template <>
struct StructTraits<
    content_settings::mojom::RendererContentSettingRulesDataView,
    RendererContentSettingRules>
    : public StructTraits<
          content_settings::mojom::RendererContentSettingRulesDataView,
          RendererContentSettingRules_ChromiumImpl> {
  static const std::vector<ContentSettingPatternSource>& autoplay_rules(
      const RendererContentSettingRules& r) {
    return r.autoplay_rules;
  }
  static const std::vector<ContentSettingPatternSource>& fingerprinting_rules(
      const RendererContentSettingRules& r) {
    return r.fingerprinting_rules;
  }
  static const std::vector<ContentSettingPatternSource>& brave_shields_rules(
      const RendererContentSettingRules& r) {
    return r.brave_shields_rules;
  }
  static const std::vector<ContentSettingPatternSource>&
  cosmetic_filtering_rules(const RendererContentSettingRules& r) {
    return r.cosmetic_filtering_rules;
  }
  static const std::map<ContentSettingsType,
                        std::vector<ContentSettingPatternSource>>&
  webcompat_rules(const RendererContentSettingRules& r) {
    return r.webcompat_rules;
  }

  static bool Read(
      content_settings::mojom::RendererContentSettingRulesDataView data,
      RendererContentSettingRules* out);
};


```

