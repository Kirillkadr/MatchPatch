### match
```
...
#include "base/time/time.h"

 #include "base/version.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```
#include "brave/browser/component_updater/brave_component_updater_configurator.h"

```

### match
```
...
>>>
 MakeChromeComponentUpdaterConfigurator 
 ( 
 const base::CommandLine* cmdline 
 ,  <<< ... 
PrefService* pref_service
 ... ) ...  
```
### patch
```
 MakeChromeComponentUpdaterConfigurator_ChromiumImpl(const base::CommandLine* cmdline,

```

### match
```
...
 namespace component_updater { ... 
 scoped_refptr<update_client::Configurator>
 MakeChromeComponentUpdaterConfigurator_ChromiumImpl(const base::CommandLine* cmdline,
PrefService* pref_service) { ... 
return base::MakeRefCounted<ChromeConfigurator>(cmdline, pref_service);
 } 
 >>> 
 ... } ...  
```
### patch
```
scoped_refptr<update_client::Configurator>
MakeChromeComponentUpdaterConfigurator(const base::CommandLine* cmdline,
                                       PrefService* pref_service) {
  return base::MakeRefCounted<BraveConfigurator>(
      cmdline, pref_service,
      g_browser_process->system_network_context_manager()
          ->GetSharedURLLoaderFactory());
}


```

