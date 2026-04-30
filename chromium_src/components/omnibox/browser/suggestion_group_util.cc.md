### match
```cpp
...
#include "components/omnibox/browser/suggestion_group_util.h"

 #include <optional>
 
 >>> 
#include "base/feature_list.h"

 ... 
```
### patch
```cpp
#include "brave/components/commander/common/buildflags/buildflags.h"
#include "components/grit/brave_components_strings.h"

```

### match
```cpp
...
 
 namespace omnibox { ... 
 
 namespace { ...   >>> 
 const 
 GroupConfigMap 
 & BuildDefaultGroups() 
 {  <<< 
if (g_default_groups.Get().empty()) {
    g_default_groups.Get() = {
        // clang-format off
        {GROUP_MOBILE_SEARCH_READY_OMNIBOX, CreateGroup(SECTION_MOBILE_VERBATIM)},
        {GROUP_MOBILE_CLIPBOARD,            CreateGroup(SECTION_MOBILE_CLIPBOARD)},
        {GROUP_PERSONALIZED_ZERO_SUGGEST,   CreateGroup(SECTION_PERSONALIZED_ZERO_SUGGEST)},
        {GROUP_MOBILE_MOST_VISITED,
         CreateGroup(SECTION_MOBILE_MOST_VISITED,
                     base::FeatureList::IsEnabled(
                         kMostVisitedTilesHorizontalRenderGroup)
                         ? GroupConfig_RenderType_HORIZONTAL
                         : GroupConfig_RenderType_DEFAULT_VERTICAL)},

        {GROUP_MOBILE_RICH_ANSWER,
         CreateGroup(SECTION_SEARCH)},
        {GROUP_SEARCH, CreateGroup(SECTION_SEARCH)},
        {GROUP_OTHER_NAVS, CreateGroup(SECTION_SEARCH)},
        // clang-format on
    };
  }
 ... } ...  } ...  } ...  
```
### patch
```cpp
const GroupConfigMap& BuildDefaultGroups_ChromiumImplBuildDefaultGroups_ChromiumImpl() {

```

### match
```cpp
...
 
 namespace omnibox { ... 
 
 const omnibox::GroupConfigMap& BuildDefaultGroupsForInput(
    const AutocompleteInput& input,
    bool is_incognito) { ... 
 
 default : ...   >>> 
 return BuildDefaultGroups();  <<<  ...} ...  } ...  
```
### patch
```cpp
      return BuildDefaultGroups_ChromiumImplBuildDefaultGroups_ChromiumImpl();

```

### match
```cpp
...
 
 namespace omnibox { ... 
 
 GroupId GroupIdForNumber(int value) { ... 
return GroupId_IsValid(value) ? static_cast<GroupId>(value) : GROUP_INVALID;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
const GroupConfigMap& BuildDefaultGroups() {
  if (g_default_groups.Get().empty()) {
    BuildDefaultGroups_ChromiumImpl();
#if BUILDFLAG(ENABLE_COMMANDER)
    g_default_groups.Get()[GROUP_OTHER_NAVS] = CreateGroup(
        SECTION_OTHER_NAVS,
        GroupConfig::RenderType::GroupConfig_RenderType_DEFAULT_VERTICAL,
        IDS_IDC_COMMANDER);
#endif
  }

  return g_default_groups.Get();
}

```

