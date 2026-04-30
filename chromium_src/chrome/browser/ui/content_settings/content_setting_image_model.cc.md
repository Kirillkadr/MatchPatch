### match
```cpp
...
#include "base/metrics/user_metrics.h"

 #include "base/metrics/user_metrics_action.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/ui/content_settings/brave_content_setting_image_models.h"
#include "brave/components/vector_icons/vector_icons.h"

```

### match
```cpp
...
std::vector<std::unique_ptr<ContentSettingImageModel>>  >>> 
 ContentSettingImageModel::GenerateContentSettingImageModels() 
 {  <<< 
// The ordering of the models here influences the order in which icons are
 ... } ...  
```
### patch
```cpp
ContentSettingImageModel::GenerateContentSettingImageModels_ChromiumImpl() {

```

### match
```cpp
...
 
 size_t ContentSettingImageModel::GetContentSettingImageModelIndexForTesting(
    ImageType image_type) { ...   >>> 
 GenerateContentSettingImageModels() 
 ;  <<<  ...} ...  
```
### patch
```cpp
      GenerateContentSettingImageModels_ChromiumImpl();

```

### match
```cpp
...
 
 size_t ContentSettingImageModel::GetContentSettingImageModelIndexForTesting(
    ImageType image_type) { ... 
NOTREACHED();
 } 
 >>> 
 ... 
```
### patch
```cpp

 std::vector<std::unique_ptr<ContentSettingImageModel>>
ContentSettingImageModel::GenerateContentSettingImageModels() {
  std::vector<std::unique_ptr<ContentSettingImageModel>> result =
      GenerateContentSettingImageModels_ChromiumImpl();
  BraveGenerateContentSettingImageModels(&result);
  return result;
}

void ContentSettingImageModel::GetIconFromType(
    ContentSettingsType type,
    bool blocked,
    raw_ptr<const gfx::VectorIcon>* icon,
    raw_ptr<const gfx::VectorIcon>* badge) {
  if (type == ContentSettingsType::AUTOPLAY) {
    *badge = (blocked ? &vector_icons::kBlockedBadgeIcon
                      : &gfx::VectorIcon::EmptyIcon());
    *icon = &kAutoplayStatusIcon;
  } else {
    ::GetIconFromType(type, blocked, icon, badge);
  }
}

```

