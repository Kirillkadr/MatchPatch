### match
```cpp
...
#include "base/trace_event/trace_event.h"

 #include "base/version_info/version_info.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/profiles/brave_profile_manager.h"
#include "brave/components/ai_chat/core/common/buildflags/buildflags.h"

```

### match
```cpp
...
#include "google_apis/gaia/gaia_auth_util.h"

 #include "ui/base/l10n/l10n_util.h"
 
 >>> 
#if BUILDFLAG(ENABLE_EXTENSIONS_CORE)
#include "extensions/browser/extension_system.h"
#endif
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_AI_CHAT)
#include "brave/components/ai_chat/core/common/features.h"
#endif

// static
std::vector<Profile*> ProfileManager::GetLastOpenedProfiles() {
  // Don't include AI Chat agent profile in the list, to avoid
  // re-opening it on startup and having users mistake it for their
  // main profile, adding authentication they might not want exposed
  // to the agent.
  // Alternatives considered:
  // - Intercepting SaveActiveProfiles. Problematic because we would either have
  // to first remove the profile from `active_profiles_` (which
  // `OnBrowserClosed` expects the profile to be in the list), or perform a
  // quick subsequent pref update (which could cause side effects).
  std::vector<Profile*> profiles = GetLastOpenedProfiles_ChromiumImpl();
#if BUILDFLAG(ENABLE_BRAVE_AI_CHAT_AGENT_PROFILE)
  if (ai_chat::features::IsAIChatAgentProfileEnabled()) {
    std::erase_if(profiles,
                  [](Profile* profile) { return profile->IsAIChatAgent(); });
  }
#endif
  return profiles;
}


```

### match
```cpp
...
>>>
 std::vector<Profile*> 
 ProfileManager::GetLastOpenedProfiles() 
 {  <<< 
ProfileManager* profile_manager = g_browser_process->profile_manager();
 ... } ...  
```
### patch
```cpp
std::vector<Profile*> ProfileManager::GetLastOpenedProfiles_ChromiumImpl() {

```

