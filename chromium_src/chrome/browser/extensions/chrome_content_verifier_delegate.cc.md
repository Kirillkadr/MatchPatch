### match
```
...
#include "base/metrics/field_trial.h"

 #include "base/metrics/histogram_functions.h"
 
 >>> 
#include "base/strings/escape.h"

 ... 
```
### patch
```
#include "base/no_destructor.h"

```

### match
```
...
#include "chrome/browser/extensions/corrupted_extension_reinstaller.h"

 #include "chrome/browser/extensions/extension_management.h"
 
 >>> 
#include "chrome/common/chrome_switches.h"

 ... 
```
### patch
```
#include "chrome/browser/extensions/extension_service.h"

```

### match
```
...
#include "chrome/browser/extensions/extension_assets_manager_chromeos.h"

 #endif 
 >>> 
 ... 
```
### patch
```
#if defined(OFFICIAL_BUILD)
#undef BUILDFLAG_INTERNAL_GOOGLE_CHROME_BRANDING
#define BUILDFLAG_INTERNAL_GOOGLE_CHROME_BRANDING() (1)
#endif

```

### match
```
...
 
 namespace extensions { ... 
ChromeContentVerifierDelegate::VerifyInfo
ChromeContentVerifierDelegate::GetVerifyInfo(const Extension& extension) const {
  if (g_verify_info_test_callback) {
    return g_verify_info_test_callback->Run(extension);
  }

  ManagementPolicy* management_policy =
      ExtensionSystem::Get(context_)->management_policy();

  // Magement policy may be not configured in some tests.
  bool should_repair =
      (management_policy &&
       management_policy->ShouldRepairIfCorrupted(&extension)) ||
      base::CommandLine::ForCurrentProcess()->HasSwitch(
          ::switches::kRepairAllValidExtensions);
  bool is_from_webstore = IsFromWebstore(extension);

#if BUILDFLAG(IS_CHROMEOS)
  if (ExtensionAssetsManagerChromeOS::IsSharedInstall(&extension)) {
    return VerifyInfo(VerifyInfo::Mode::ENFORCE_STRICT, is_from_webstore,
                      should_repair);
  }
#endif

  if (should_repair)
    return VerifyInfo(default_mode_, is_from_webstore, should_repair);

  if (!extension.is_extension() && !extension.is_legacy_packaged_app())
    return VerifyInfo(VerifyInfo::Mode::NONE, is_from_webstore, should_repair);
  if (!Manifest::IsAutoUpdateableLocation(extension.location()))
    return VerifyInfo(VerifyInfo::Mode::NONE, is_from_webstore, should_repair);
  if (!is_from_webstore)
    return VerifyInfo(VerifyInfo::Mode::NONE, is_from_webstore, should_repair);

  return VerifyInfo(default_mode_, is_from_webstore, should_repair);
}
 } 
 // namespace extensions 
 >>> 
 ... 
```
### patch
```
#if defined(OFFICIAL_BUILD)
#undef BUILDFLAG_INTERNAL_GOOGLE_CHROME_BRANDING
#endif
```

