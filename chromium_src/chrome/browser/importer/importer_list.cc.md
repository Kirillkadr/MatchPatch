### match
```
...
#include "chrome/browser/importer/importer_list.h"

 #include <stdint.h>
 
 >>> 
#include "base/functional/bind.h"

 ... 
```
### patch
```
#include "base/check.h"
#include "base/files/file_path.h"

```

### match
```
...
#include "base/files/file_path.h"

 #include "base/functional/bind.h"
 
 >>> 
#include "base/task/task_traits.h"

 ... 
```
### patch
```
#include "base/strings/strcat.h"
#include "base/strings/utf_string_conversions.h"

```

### match
```
...
#include "base/task/thread_pool.h"

 #include "base/threading/scoped_blocking_call.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "base/values.h"
#include "brave/common/importer/chrome_importer_utils.h"
#include "brave/common/importer/importer_constants.h"
#include "brave/grit/brave_generated_resources.h"

```

### match
```
...
#include "chrome/grit/generated_resources.h"

 #include "components/user_data_importer/common/importer_data_types.h"
 
 >>> 
#include "ui/base/l10n/l10n_util.h"

 ... 
```
### patch
```
#include "components/user_data_importer/common/importer_type.h"

```

### match
```
...
 namespace 
 { 
 >>> 
#if BUILDFLAG(IS_WIN)
void DetectIEProfiles(
    std::vector<user_data_importer::SourceProfile>* profiles) {
  base::ScopedBlockingCall scoped_blocking_call(FROM_HERE,
                                                base::BlockingType::MAY_BLOCK);

  // IE always exists and doesn't have multiple profiles.
  user_data_importer::SourceProfile ie;
  ie.importer_name = l10n_util::GetStringUTF16(IDS_IMPORT_FROM_IE);
  ie.importer_type = user_data_importer::TYPE_IE;
  ie.services_supported = user_data_importer::HISTORY |
                          user_data_importer::FAVORITES |
                          user_data_importer::SEARCH_ENGINES;
  profiles->push_back(ie);
}

void DetectEdgeProfiles(
    std::vector<user_data_importer::SourceProfile>* profiles) {
  if (!importer::EdgeImporterCanImport()) {
    return;
  }
  user_data_importer::SourceProfile edge;
  edge.importer_name = l10n_util::GetStringUTF16(IDS_IMPORT_FROM_EDGE);
  edge.importer_type = user_data_importer::TYPE_EDGE;
  edge.services_supported = user_data_importer::FAVORITES;
  edge.source_path = importer::GetEdgeDataFilePath();
  profiles->push_back(edge);
}

void DetectBuiltinWindowsProfiles(
    std::vector<user_data_importer::SourceProfile>* profiles) {
  if (shell_integration::IsIEDefaultBrowser()) {
    DetectIEProfiles(profiles);
    DetectEdgeProfiles(profiles);
  } else {
    DetectEdgeProfiles(profiles);
    DetectIEProfiles(profiles);
  }
}

#endif
 ... } ...  
```
### patch
```
void AddChromeToProfiles(
    std::vector<user_data_importer::SourceProfile>* profiles,
    base::ListValue chrome_profiles,
    const base::FilePath& user_data_folder,
    const std::string& brand,
    user_data_importer::ImporterType type) {
  for (const auto& value : chrome_profiles) {
    const auto* dict = value.GetIfDict();
    if (!dict) {
      continue;
    }
    uint16_t items = user_data_importer::NONE;
    auto* profile = dict->FindString("id");
    auto* name = dict->FindString("name");
    DCHECK(profile);
    DCHECK(name);
    base::FilePath path = user_data_folder;
    if (!ChromeImporterCanImport(path.Append(base::FilePath::StringType(
                                     profile->begin(), profile->end())),
                                 type, &items)) {
      continue;
    }
    user_data_importer::SourceProfile chrome;
    chrome.importer_name = base::UTF8ToUTF16(base::StrCat({brand, " ", *name}));
    chrome.importer_type = type;
    chrome.services_supported = items;
    chrome.source_path = user_data_folder.Append(
        base::FilePath::StringType(profile->begin(), profile->end()));
    profiles->push_back(chrome);
  }
}

void DetectChromeProfiles(
    std::vector<user_data_importer::SourceProfile>* profiles) {
  base::ScopedBlockingCall scoped_blocking_call(FROM_HERE,
                                                base::BlockingType::WILL_BLOCK);
  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetChromeUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetChromeUserDataFolder(), kGoogleChromeBrowser,
      user_data_importer::TYPE_CHROME);
  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetChromeBetaUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetChromeBetaUserDataFolder(), kGoogleChromeBrowserBeta,
      user_data_importer::TYPE_CHROME);
  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetChromeDevUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetChromeDevUserDataFolder(), kGoogleChromeBrowserDev,
      user_data_importer::TYPE_CHROME);
#if !BUILDFLAG(IS_LINUX)
  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetCanaryUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetCanaryUserDataFolder(), kGoogleChromeBrowserCanary,
      user_data_importer::TYPE_CHROME);
#endif
  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetChromiumUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetChromiumUserDataFolder(), kChromiumBrowser,
      user_data_importer::TYPE_CHROME);

  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetEdgeUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetEdgeUserDataFolder(), kMicrosoftEdgeBrowser,
      user_data_importer::TYPE_EDGE_CHROMIUM);

  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetVivaldiUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetVivaldiUserDataFolder(), kVivaldiBrowser,
      user_data_importer::TYPE_VIVALDI);

  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetOperaUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetOperaUserDataFolder(), kOperaBrowser, user_data_importer::TYPE_OPERA);

  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetYandexUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetYandexUserDataFolder(), kYandexBrowser,
      user_data_importer::TYPE_YANDEX);

  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetWhaleUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetWhaleUserDataFolder(), kWhaleBrowser, user_data_importer::TYPE_WHALE);

#if BUILDFLAG(IS_LINUX)
  // Installed via snap Opera has different profile path.
  AddChromeToProfiles(
      profiles,
      GetChromeSourceProfiles(GetOperaSnapUserDataFolder().Append(
          base::FilePath::StringType(FILE_PATH_LITERAL("Local State")))),
      GetOperaSnapUserDataFolder(), kOperaBrowser,
      user_data_importer::TYPE_OPERA);
#endif
}


```

### match
```
...
 
 namespace { ... 
 
 #if BUILDFLAG(IS_WIN ) ... 
 
 void DetectEdgeProfiles(
    std::vector<user_data_importer::SourceProfile>* profiles) { ... 
user_data_importer::SourceProfile edge;  >>> 
 edge.importer_name = l10n_util::GetStringUTF16(IDS_IMPORT_FROM_EDGE);  <<< 
edge.importer_type = user_data_importer::TYPE_EDGE;
 ... } ...  } ...  
```
### patch
```
  edge.importer_name = l10n_util::GetStringUTF16(IDS_BRAVE_IMPORT_FROM_EDGE);

```

