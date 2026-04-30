### match
```cpp
...
// found in the LICENSE file.
 #include "components/permissions/features.h"
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include "base/feature_override.h"

```

### match
```cpp
...
 namespace 
 features 
 { 
 >>> 
#if BUILDFLAG(IS_ANDROID)
// Enables or disables usage of Window Management Web API.
BASE_FEATURE(kAndroidWindowManagementWebApi, base::FEATURE_DISABLED_BY_DEFAULT);

// Shows or hides the cancel button in the ItemChooserDialog.
BASE_FEATURE(kAndroidItemChooserCancelButton, base::FEATURE_ENABLED_BY_DEFAULT);
#endif
 ... } ...  
```
### patch
```cpp
// Enables the option of an automatic permission expiration time.
BASE_FEATURE(kPermissionLifetime,
             base::FEATURE_ENABLED_BY_DEFAULT);

OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kCpssUseTfliteSignatureRunner, base::FEATURE_DISABLED_BY_DEFAULT},
    {kPermissionPredictionsV2, base::FEATURE_DISABLED_BY_DEFAULT},
#if !BUILDFLAG(IS_ANDROID)
    {kPermissionsPromptSurvey, base::FEATURE_DISABLED_BY_DEFAULT},
#endif
    {kShowRelatedWebsiteSetsPermissionGrants,
     base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

