### match
```
...
#include "base/logging.h"

 #include "base/notreached.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ...
```
### patch
```
#include "brave/components/brave_extension/grit/brave_extension.h"

```

### match
```
...
#include "chrome/common/extensions/extension_constants.h"

 #include "chrome/grit/browser_resources.h"
 
 >>> 
#include "extensions/buildflags/buildflags.h"

 ...
```
### patch
```
#include "components/grit/brave_components_resources.h"

```

### match
```
...
 
 namespace extensions { ...   >>> 
 bool 
 IsComponentExtensionAllowlisted(const std::string& extension_id) 
 {  <<< 
constexpr auto kAllowed = base::MakeFixedFlatSet<std::string_view>({
      extension_misc::kInAppPaymentsSupportAppId,
      extension_misc::kPdfExtensionId,
#if BUILDFLAG(IS_CHROMEOS)
      extension_misc::kAssessmentAssistantExtensionId,
      extension_misc::kAccessibilityCommonExtensionId,
      extension_misc::kChromeVoxExtensionId,
      extension_misc::kEnhancedNetworkTtsExtensionId,
      extension_misc::kEspeakSpeechSynthesisExtensionId,
      extension_misc::kGoogleSpeechSynthesisExtensionId,
      extension_misc::kGuestModeTestExtensionId,
      extension_misc::kSelectToSpeakExtensionId,
      extension_misc::kSwitchAccessExtensionId,
      extension_misc::kContactCenterInsightsExtensionId,
      extension_misc::kDeskApiExtensionId,
#if BUILDFLAG(GOOGLE_CHROME_BRANDING)
      extension_misc::kQuickOfficeComponentExtensionId,
#endif  // BUILDFLAG(GOOGLE_CHROME_BRANDING)
#endif  // BUILDFLAG(IS_CHROMEOS)
      extension_misc::kReadingModeGDocsHelperExtensionId,
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_MAC)
      extension_misc::kTTSEngineExtensionId,
      extension_misc::kComponentUpdaterTTSEngineExtensionId,
#endif  // BUILDFLAG(IS_WIN) || BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_MAC)
  });

  if (kAllowed.contains(extension_id)) {
    return true;
  }

#if BUILDFLAG(IS_CHROMEOS)
  if (chromeos::features::IsUploadOfficeToCloudEnabled() &&
      extension_id == extension_misc::kODFSExtensionId) {
    return true;
  }

  if (ash::input_method::ComponentExtensionIMEManagerDelegateImpl::
          IsIMEExtensionID(extension_id)) {
    return true;
  }
#endif  // BUILDFLAG(IS_CHROMEOS)
  LOG(ERROR) << "Component extension with id " << extension_id << " not in "
             << "allowlist and is not being loaded as a result.";
  NOTREACHED() << "Component extension with id " << extension_id << " not in "
               << "allowlist and is not being loaded as a result.";
}

bool IsComponentExtensionAllowlisted(int manifest_resource_id)
 ... } ...
```
### patch
```
bool IsComponentExtensionAllowlisted_ChromiumImpl(const std::string& extension_id) {

```

### match
```
...
 
 namespace extensions { ... 
 
 bool IsComponentExtensionAllowlisted_ChromiumImpl(const std::string& extension_id) { ... 
 
 base::MakeFixedFlatSet<std::string_view> ( ... 
{
      extension_misc::kInAppPaymentsSupportAppId,
      extension_misc::kPdfExtensionId,
#if BUILDFLAG(IS_CHROMEOS)
      extension_misc::kAssessmentAssistantExtensionId,
      extension_misc::kAccessibilityCommonExtensionId,
      extension_misc::kChromeVoxExtensionId,
      extension_misc::kEnhancedNetworkTtsExtensionId,
      extension_misc::kEspeakSpeechSynthesisExtensionId,
      extension_misc::kGoogleSpeechSynthesisExtensionId,
      extension_misc::kGuestModeTestExtensionId,
      extension_misc::kSelectToSpeakExtensionId,
      extension_misc::kSwitchAccessExtensionId,
      extension_misc::kContactCenterInsightsExtensionId,
      extension_misc::kDeskApiExtensionId,
#if BUILDFLAG(GOOGLE_CHROME_BRANDING)
      extension_misc::kQuickOfficeComponentExtensionId,
#endif  // BUILDFLAG(GOOGLE_CHROME_BRANDING)
#endif  // BUILDFLAG(IS_CHROMEOS)
      extension_misc::kReadingModeGDocsHelperExtensionId,
#if BUILDFLAG(IS_WIN) || BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_MAC)
      extension_misc::kTTSEngineExtensionId,
      extension_misc::kComponentUpdaterTTSEngineExtensionId,
#endif  // BUILDFLAG(IS_WIN) || BUILDFLAG(IS_LINUX) || BUILDFLAG(IS_MAC)
  });

  if (kAllowed.contains(extension_id)) {
    return true;
  }

#if BUILDFLAG(IS_CHROMEOS)
  if (chromeos::features::IsUploadOfficeToCloudEnabled() &&
      extension_id == extension_misc::kODFSExtensionId) {
    return true;
  }

  if (ash::input_method::ComponentExtensionIMEManagerDelegateImpl::
          IsIMEExtensionID(extension_id)) {
    return true;
  }
#endif  // BUILDFLAG(IS_CHROMEOS)
  LOG(ERROR) << "Component extension with id " << extension_id << " not in "
             << "allowlist and is not being loaded as a result.";
  NOTREACHED() << "Component extension with id " << extension_id << " not in "
               << "allowlist and is not being loaded as a result.";
}  >>> 
 bool IsComponentExtensionAllowlisted(int manifest_resource_id 
 ) 
  
 {  <<< 
switch (manifest_resource_id) {
    // Please keep the list in alphabetical order.
#if BUILDFLAG(ENABLE_HANGOUT_SERVICES_EXTENSION)
    case IDR_HANGOUT_SERVICES_MANIFEST_V2:
    case IDR_HANGOUT_SERVICES_MANIFEST_V3:
#endif
    case IDR_NETWORK_SPEECH_SYNTHESIS_MANIFEST:
    case IDR_NETWORK_SPEECH_SYNTHESIS_MANIFEST_MV3:
    case IDR_READING_MODE_GDOCS_HELPER_MANIFEST:
    case IDR_WEBSTORE_MANIFEST:

#if BUILDFLAG(IS_CHROMEOS)
    // Separate ChromeOS list, as it is quite large.
    case IDR_ARC_SUPPORT_MANIFEST:
    case IDR_CHROME_APP_MANIFEST:
    case IDR_IMAGE_LOADER_MANIFEST:
    case IDR_KEYBOARD_MANIFEST:
#if BUILDFLAG(GOOGLE_CHROME_BRANDING)
    case IDR_HELP_MANIFEST:
#endif  // BUILDFLAG(GOOGLE_CHROME_BRANDING)
    case IDR_CONTACT_CENTER_INSIGHTS_MANIFEST:
    case IDR_DESK_API_MANIFEST:
    case IDR_ECHO_MANIFEST:
#endif  // BUILDFLAG(IS_CHROMEOS)
      return true;
  }
 ... } ...  } ...
```
### patch
```
bool IsComponentExtensionAllowlisted_ChromiumImpl(int manifest_resource_id) {

```

### match
```
...
 
 namespace extensions { ... 
 
bool IsComponentExtensionAllowlistedForSignInProfile(
    const std::string& extension_id) {
  constexpr auto kAllowed = base::MakeFixedFlatSet<std::string_view>({
      extension_misc::kAccessibilityCommonExtensionId,
      extension_misc::kChromeVoxExtensionId,
      extension_misc::kEspeakSpeechSynthesisExtensionId,
      extension_misc::kGoogleSpeechSynthesisExtensionId,
      extension_misc::kSelectToSpeakExtensionId,
      extension_misc::kSwitchAccessExtensionId,
  });

  return kAllowed.contains(extension_id);
}
 #endif 
 >>> 
 ... } ...
```
### patch
```
bool IsComponentExtensionAllowlisted(const std::string& extension_id) {
    const char* const kAllowed[] = {brave_extension_id};

    for (const auto* id : kAllowed) {
      if (extension_id == id) {
        return true;
      }
    }

    return IsComponentExtensionAllowlisted_ChromiumImpl(extension_id);
  }

  bool IsComponentExtensionAllowlisted(int manifest_resource_id) {
    switch (manifest_resource_id) {
      // Please keep the list in alphabetical order.
      case IDR_BRAVE_EXTENSION:
        return true;
    }

    return IsComponentExtensionAllowlisted_ChromiumImpl(manifest_resource_id);
  }


```

