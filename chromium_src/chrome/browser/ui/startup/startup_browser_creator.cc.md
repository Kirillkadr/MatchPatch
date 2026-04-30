### match
```cpp
...
#include "base/threading/scoped_blocking_call.h"

 #include "base/trace_event/trace_event.h"
 
 >>> 
#include "build/branding_buildflags.h"

 ... 
```
### patch
```cpp
#include "brave/components/constants/brave_switches.h"
#include "brave/components/tor/buildflags/buildflags.h"

```

### match
```cpp
...
#include "chrome/browser/ui/startup/focus/focus_handler.h"

 #endif 
 >>> 
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_TOR)
#include "brave/browser/tor/tor_profile_manager.h"
#endif

#ifdef LaunchModeRecorder
static_assert(false,
              "Replace the use of OldLaunchModeRecorder with "
              "LaunchModeRecorder, and remove this assert.");
#endif  // #ifdef LaunchModeRecorder


```

### match
```cpp
...
 
 namespace { ... 
 } 
 // namespace 
 >>> 
StartupBrowserCreator::StartupBrowserCreator() = default;
 ... 
```
### patch
```cpp
class BraveStartupBrowserCreatorImpl final : public StartupBrowserCreatorImpl {
 public:
  BraveStartupBrowserCreatorImpl(const base::FilePath& cur_dir,
                                 const base::CommandLine& command_line,
                                 chrome::startup::IsFirstRun is_first_run);

  BraveStartupBrowserCreatorImpl(const base::FilePath& cur_dir,
                                 const base::CommandLine& command_line,
                                 StartupBrowserCreator* browser_creator,
                                 chrome::startup::IsFirstRun is_first_run);

  void Launch(Profile* profile,
              chrome::startup::IsProcessStartup process_startup,
              bool restore_tabbed_browser);

  void MaybeShowNonMilestoneUpdateToast(
      Browser* browser,
      const std::string& current_version_string) override {}
};

BraveStartupBrowserCreatorImpl::BraveStartupBrowserCreatorImpl(
    const base::FilePath& cur_dir,
    const base::CommandLine& command_line,
    chrome::startup::IsFirstRun is_first_run)
    : StartupBrowserCreatorImpl(cur_dir, command_line, is_first_run) {}

BraveStartupBrowserCreatorImpl::BraveStartupBrowserCreatorImpl(
    const base::FilePath& cur_dir,
    const base::CommandLine& command_line,
    StartupBrowserCreator* browser_creator,
    chrome::startup::IsFirstRun is_first_run)
    : StartupBrowserCreatorImpl(cur_dir,
                                command_line,
                                browser_creator,
                                is_first_run) {}

// If the --tor command line flag was provided, switch the profile to Tor mode
// and then call the original Launch method.
//
// This switch is primarily used for testing and is not the same as using the
// Tor browser. In particular, you will see some profile-wide network traffic
// not going through the tor proxy (e.g. adblock list updates, P3A).
//
// Note that if the --tor switch is used together with --silent-launch, Tor
// won't be launched.
void BraveStartupBrowserCreatorImpl::Launch(
    Profile* profile,
    chrome::startup::IsProcessStartup process_startup,
    bool restore_tabbed_browser) {
#if BUILDFLAG(ENABLE_TOR)
  if (StartupBrowserCreatorImpl::command_line_->HasSwitch(switches::kTor)) {
    // Call StartupBrowserCreatorImpl::Launch() with the Tor profile so that if
    // one runs brave-browser --tor "? search query" the search query is not
    // passed to the default search engine of the regular profile.
    LOG(INFO) << "Switching to Tor profile and starting Tor service.";
    profile = TorProfileManager::GetInstance().GetTorProfile(profile);
  }
#endif

  StartupBrowserCreatorImpl::Launch(profile, process_startup,
                                    restore_tabbed_browser);
}


```

### match
```cpp
...
 
 
 if (!IsSilentLaunchEnabled(command_line, profile)) { ... 
 >>> 
 StartupBrowserCreatorImpl lwp(cur_dir, command_line, this, is_first_run);  <<< 

 ... } ...   
```
### patch
```cpp
    BraveStartupBrowserCreatorImpl lwp(cur_dir, command_line, this, is_first_run);

```

### match
```cpp
...
>>>
 StartupBrowserCreatorImpl 
 startup_browser_creator_impl 
 (  <<< 
base::FilePath()
 ... ) ...  
```
### patch
```cpp
  BraveStartupBrowserCreatorImpl startup_browser_creator_impl(

```

