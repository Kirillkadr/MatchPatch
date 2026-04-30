### match
```cpp
...
#import "ui/base/device_form_factor.h"

 #import "ui/base/l10n/l10n_util.h"
 
 >>> 
namespace {

web::WebUIIOSDataSource* CreateVersionUIDataSource() {
  web::WebUIIOSDataSource* html_source =
      web::WebUIIOSDataSource::Create(kChromeUIVersionHost);

  // Localized and data strings.
  html_source->AddLocalizedString(version_ui::kTitle, IDS_VERSION_UI_TITLE);
  html_source->AddLocalizedString(version_ui::kLogoAltText,
                                  IDS_SHORT_PRODUCT_LOGO_ALT_TEXT);
  html_source->AddLocalizedString(version_ui::kApplicationLabel,
                                  IDS_IOS_PRODUCT_NAME);
  html_source->AddString(version_ui::kVersion,
                         std::string(version_info::GetVersionNumber()));
  html_source->AddString(version_ui::kVersionModifier,
                         std::string(GetChannelString(GetChannel())));
  html_source->AddLocalizedString(version_ui::kOSName, IDS_VERSION_UI_OS);
  html_source->AddString(version_ui::kOSType,
                         std::string(version_info::GetOSType()));

  // Always empty on iOS.
  html_source->AddString(version_ui::kVersionSuffix, std::string());

  html_source->AddLocalizedString(version_ui::kCompany,
                                  IDS_IOS_ABOUT_VERSION_COMPANY_NAME);
  html_source->AddLocalizedString(version_ui::kCopyLabel,
                                  IDS_VERSION_UI_COPY_LABEL);
  html_source->AddLocalizedString(version_ui::kCopyNotice,
                                  IDS_VERSION_UI_COPY_NOTICE);
  html_source->AddString(
      version_ui::kCopyright,
      l10n_util::GetStringFUTF16(
          IDS_IOS_ABOUT_VERSION_COPYRIGHT,
          base::LocalizedTimeFormatWithPattern(base::Time::Now(), "y")));
  html_source->AddLocalizedString(version_ui::kRevision,
                                  IDS_VERSION_UI_REVISION);
  std::string last_change(version_info::GetLastChange());
  // Shorten the git hash to display it correctly on small devices.
  if ((ui::GetDeviceFormFactor() != ui::DEVICE_FORM_FACTOR_TABLET) &&
      last_change.length() > 12) {
    last_change =
        base::StringPrintf("%s...", last_change.substr(0, 12).c_str());
  }
  html_source->AddString(version_ui::kCL, last_change);
  html_source->AddLocalizedString(version_ui::kOfficial,
                                  version_info::IsOfficialBuild()
                                      ? IDS_VERSION_UI_OFFICIAL
                                      : IDS_VERSION_UI_UNOFFICIAL);
  html_source->AddLocalizedString(
      version_ui::kVersionProcessorVariation,
      sizeof(void*) == 8 ? IDS_VERSION_UI_64BIT : IDS_VERSION_UI_32BIT);
  html_source->AddLocalizedString(version_ui::kUserAgentName,
                                  IDS_VERSION_UI_USER_AGENT);
  html_source->AddString(
      version_ui::kUserAgent,
      web::GetWebClient()->GetUserAgent(web::UserAgentType::MOBILE));
  html_source->AddLocalizedString(version_ui::kCommandLineName,
                                  IDS_VERSION_UI_COMMAND_LINE);

  std::string command_line;
  typedef std::vector<std::string> ArgvList;
  const ArgvList& argv = base::CommandLine::ForCurrentProcess()->argv();
  for (ArgvList::const_iterator iter = argv.begin(); iter != argv.end();
       iter++) {
    command_line += " " + *iter;
  }
  // This assumes that `command_line` uses UTF-8 encoding.
  html_source->AddString(version_ui::kCommandLine, command_line);

  html_source->AddLocalizedString(version_ui::kVariationsName,
                                  IDS_VERSION_UI_VARIATIONS);
  html_source->AddLocalizedString(version_ui::kVariationsCmdName,
                                  IDS_VERSION_UI_VARIATIONS_CMD);
  html_source->AddLocalizedString(version_ui::kCopyVariationsLabel,
                                  IDS_VERSION_UI_COPY_VARIATIONS_LABEL);
  html_source->AddLocalizedString(version_ui::kCopyVariationsNotice,
                                  IDS_VERSION_UI_COPY_VARIATIONS_NOTICE);
  html_source->AddLocalizedString(version_ui::kVariationsSeedName,
                                  IDS_VERSION_UI_VARIATIONS_SEED_NAME);

  html_source->AddString(
      version_ui::kVariationsSeed,
      version_ui::SeedTypeToUiString(
          GetApplicationContext()->GetVariationsService()->GetSeedType()));

  html_source->AddString(version_ui::kSanitizer,
                         std::string(version_info::GetSanitizerList()));

  html_source->UseStringsJs();
  html_source->AddResourcePaths(kVersionUiResources);
  html_source->AddResourcePath("images/product_logo.png", IDR_PRODUCT_LOGO);
  html_source->AddResourcePath("images/product_logo_white.png",
                               IDR_PRODUCT_LOGO_WHITE);
  html_source->SetDefaultResource(IDR_VERSION_UI_ABOUT_VERSION_HTML);
  return html_source;
}

}
 ... 
```
### patch
```cpp
#include "brave/components/version_info/version_info.h"
#include "components/version_info/version_info.h"

```

### match
```cpp
...
 
 namespace { ... 
 
 web::WebUIIOSDataSource* CreateVersionUIDataSource() { ... 
 
 html_source->AddString ( ...   >>> 
 std::string(version_info::GetVersionNumber()) 
 ) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
                         std::string(version_info::GetBraveVersionNumberForDisplay()));

```

