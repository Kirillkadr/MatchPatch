### match
```cpp
...
#include "chrome/browser/first_run/first_run.h"

 #include "chrome/browser/profiles/profile.h"
 
 >>> 
#include "chrome/browser/profiles/profile_selections.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/profiles/profile_attributes_entry.h"
#include "chrome/browser/profiles/profile_attributes_storage.h"
#include "chrome/browser/profiles/profile_manager.h"

```

### match
```cpp
...
 
 void FirstRunService::FinishProfileSetUp(std::u16string profile_name) { ... 
DCHECK(!profile_name.empty());  >>> 
 FinalizeNewProfileSetup(&profile_.get(), profile_name,
                          /*is_default_name=*/false);  <<<  ...} ...  
```
### patch
```cpp
  ProfileAttributesEntry* entry =                                              
      g_browser_process->profile_manager()
          ->GetProfileAttributesStorage()
          .GetProfileAttributesWithPath(profile_->GetPath());
  CHECK(entry);
  std::u16string original_name = entry->GetLocalProfileName();
  CHECK(!original_name.empty());
  bool is_default =
      g_browser_process->profile_manager()
          ->GetProfileAttributesStorage()
          .IsDefaultProfileName(
              original_name, /*include_check_for_legacy_profile_name=*/false);
  FinalizeNewProfileSetup(&profile_.get(), original_name, is_default)

```

