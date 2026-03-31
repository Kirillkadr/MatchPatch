### match
```cpp
...
#include "extensions/common/permissions/permissions_data.h"

 #include "third_party/blink/public/common/service_worker/service_worker_status_code.h"
 
 >>> 
using content::DevToolsAgentHost;
 ... 
```
### patch
```cpp
#include "extensions/browser/extension_registrar.h"
#include "extensions/browser/api/content_settings/content_settings_service.h"

```

### match
```cpp
...
 
 namespace extensions { ...   >>> 
 void 
 ExtensionRegistrar::AddComponentExtension(const Extension* extension) 
 {  <<< 
extension_prefs_->ClearInapplicableDisableReasonsForComponentExtension(
      extension->id());
 ... } ...  } ...  
```
### patch
```cpp
void ExtensionRegistrar::AddComponentExtension_ChromiumImpl(const Extension* extension) {

```

### match
```cpp
...
 
 namespace extensions { ... 
 
 bool ExtensionRegistrar::ShouldBlockExtension(
    const Extension* extension) const { ... 
return !extension || CanBlockExtension(extension);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void ExtensionRegistrar::AddComponentExtension(const Extension* extension) {
  AddComponentExtension_ChromiumImpl(extension);
  // ContentSettingsStore::RegisterExtension is only called for default
  // components on the first run with a fresh profile. All restarts of the
  // browser after that do not call it. This causes ContentSettingsStore's
  // `entries_` to never insert the component ID and then
  // ContentSettingsStore::GetValueMap always returns nullptr. I don't think
  // Chromium is affected by this simply because they don't use content settings
  // from default component extensions.
  extension_prefs_->OnExtensionInstalled(
      extension, /*disable_reasons=*/{}, syncer::StringOrdinal(),
      extensions::kInstallFlagNone, std::string(), {} /* ruleset_checksums */);
  extensions::ContentSettingsService::Get(browser_context_)
      ->OnExtensionPrefsLoaded(extension->id(), extension_prefs_);
}

```

