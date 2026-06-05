### match
```cpp
...
// found in the LICENSE file.
 #include "components/privacy_sandbox/privacy_sandbox_features.h"
 
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
 
 namespace privacy_sandbox { ... 
 
 BASE_FEATURE ( ... 
kPrivacySandboxAdPrivacyUxDeprecation,
             
 base::FEATURE_DISABLED_BY_DEFAULT 
 ) 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
OVERRIDE_FEATURE_DEFAULT_STATES({{
    {kEnforcePrivacySandboxAttestations, base::FEATURE_DISABLED_BY_DEFAULT},
    {kOverridePrivacySandboxSettingsLocalTesting,
     base::FEATURE_DISABLED_BY_DEFAULT},
    {kPrivacySandboxSettings4, base::FEATURE_DISABLED_BY_DEFAULT},
}});

```

