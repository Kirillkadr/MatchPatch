### match
```cpp
...
#include <optional>

 #include <string>
 
 >>> 
#include "base/containers/fixed_flat_map.h"

 ... 
```
### patch
```cpp
#include "brave/components/constants/pref_names.h"
#include "components/content_settings/core/common/pref_names.h"

```

### match
```cpp
...
 
 namespace { ... 
 kPrefsForManagedContentSettingsMap[] 
 = 
 { 
 >>> 
{prefs::kManagedAutomaticFullscreenAllowedForUrls,
         ContentSettingsType::AUTOMATIC_FULLSCREEN, CONTENT_SETTING_ALLOW}
 ... } ...  } ...  
```
### patch
```cpp
        {kManagedBraveShieldsDisabledForUrls, ContentSettingsType::BRAVE_SHIELDS,    \
         CONTENT_SETTING_BLOCK},                                                     \
      {kManagedBraveShieldsEnabledForUrls, ContentSettingsType::BRAVE_SHIELDS, \
       CONTENT_SETTING_ALLOW},

```

### match
```cpp
...
 
 namespace { ... 
 constexpr 
 const 
 char 
 * kManagedPrefs[] 
 = 
 { 
 >>> 
prefs::kManagedAutomaticFullscreenAllowedForUrls
 ... } ...  } ...  
```
### patch
```cpp
kManagedBraveShieldsDisabledForUrls, kManagedBraveShieldsEnabledForUrls,

```

### match
```cpp
...
 
 namespace { ... 
 constexpr 
 const 
 char 
 * kManagedDefaultPrefs[] 
 = 
 { 
 >>> 
prefs::kManagedDefaultAdsSetting
 ... } ...  } ...  
```
### patch
```cpp
kManagedDefaultBraveFingerprintingV2,                    
      prefs::kManagedDefaultBraveHttpsUpgrade,
      prefs::kManagedDefaultBraveReferrersSetting,
      prefs::kManagedDefaultBraveRemember1PStorageSetting,
      prefs::kManagedDefaultBraveAdblockSetting,

```

