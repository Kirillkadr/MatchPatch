### match
```cpp
...
// found in the LICENSE file.
 #include "components/webui/version/version_handler_helper.h"
 
 >>> 
 ... 
```
### patch
```cpp
#include "base/strings/string_util.h"

```

### match
```cpp
...
 namespace 
 version_ui 
 { 
 >>> 
 ... } ...  
```
### patch
```cpp
// Brave always shows full variations names instead of hashes.
base::ListValue GetVariationsList() {
  std::vector<std::string> variations;
  base::FieldTrial::ActiveGroups active_groups;
  base::FieldTrialList::GetActiveFieldTrialGroups(&active_groups);

  const unsigned char kNonBreakingHyphenUTF8[] = {0xE2, 0x80, 0x91, '\0'};
  const std::string kNonBreakingHyphenUTF8String(
      reinterpret_cast<const char*>(kNonBreakingHyphenUTF8));
  for (const auto& group : active_groups) {
    std::string line = group.trial_name + ":" + group.group_name;
    base::ReplaceChars(line, "-", kNonBreakingHyphenUTF8String, &line);
    variations.push_back(line);
  }

  base::ListValue variations_list;
  const std::string& seed_version = variations::GetSeedVersion();
  if (!seed_version.empty() && seed_version != "1") {
    variations_list.Append(seed_version);
  }
  for (std::string& variation : variations) {
    variations_list.Append(std::move(variation));
  }

  return variations_list;
}

```

### match
```cpp
...
 
 namespace version_ui { ... 

// Brave always shows full variations names instead of hashes.
	base::ListValue GetVariationsList() {
	  std::vector<std::string> variations;
	  base::FieldTrial::ActiveGroups active_groups;
	  base::FieldTrialList::GetActiveFieldTrialGroups(&active_groups);

	  const unsigned char kNonBreakingHyphenUTF8[] = {0xE2, 0x80, 0x91, '\0'};
	  const std::string kNonBreakingHyphenUTF8String(
	      reinterpret_cast<const char*>(kNonBreakingHyphenUTF8));
	  for (const auto& group : active_groups) {
	    std::string line = group.trial_name + ":" + group.group_name;
	    base::ReplaceChars(line, "-", kNonBreakingHyphenUTF8String, &line);
	    variations.push_back(line);
	  }

	  base::ListValue variations_list;
	  const std::string& seed_version = variations::GetSeedVersion();
	  if (!seed_version.empty() && seed_version != "1") {
	    variations_list.Append(seed_version);
	  }
	  for (std::string& variation : variations) {
	    variations_list.Append(std::move(variation));
	  }

	  return variations_list;
	}
	namespace {

#if !defined(NDEBUG)
std::string GetActiveGroupNameAsString(
    const base::FieldTrial::ActiveGroup& group) {
  static const unsigned char kNonBreakingHyphenUTF8[] = {0xE2, 0x80, 0x91,
                                                         '\0'};
  static std::string_view kNonBreakingHyphenUTF8String(
      reinterpret_cast<const char*>(kNonBreakingHyphenUTF8));

  std::string result = group.trial_name + ":" + group.group_name;
  base::ReplaceChars(result, "-", kNonBreakingHyphenUTF8String, &result);
  return result;
}
#endif  // !defined(NDEBUG)

}  // namespace

std::string SeedTypeToUiString(variations::SeedType seed_type) {
  switch (seed_type) {
    case variations::SeedType::kRegularSeed:
      // We only display if Safe or Null seed is used.
      return std::string();
    case variations::SeedType::kSafeSeed:
      return "Safe";
    case variations::SeedType::kNullSeed:
      return "Null";
  }
}

std::string VariationsSourceToUiString(
    variations::VariationsSource variations_source) {
  std::string result = "unknown";
  switch (variations_source.type) {
    case variations::VariationsSourceType::kUnknown:
      return result;
    case variations::VariationsSourceType::kCommandLineOrAboutFlags:
      return "command line or about flags";
    case variations::VariationsSourceType::kDefaultSeed:
      result = "default seed";
      break;
    case variations::VariationsSourceType::kFieldTrialConfig:
      result = "field-trial-config";
      break;
    case variations::VariationsSourceType::kVariationsServer:
      result = "variations server";
      break;
    case variations::VariationsSourceType::kManualConfigFile:
      result = "manual config file";
      break;
  }
  if (variations_source.forced_via_command_line_or_about_flags) {
    result += " (command line or about flags)";
  }
  return result;
}


>>> 
 base::ListValue 
 GetVariationsList() 
 { 
<<< 
...} ...  } ...  
```
### patch
```cpp
base::ListValue GetVariationsList_ChromiumImpl() {

```

