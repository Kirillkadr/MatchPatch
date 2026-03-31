### match
```cpp
...
#include "chrome/browser/extensions/extension_management.h"

 #include "chrome/browser/profiles/profile.h"
 
 >>> 
#include "chrome/browser/safe_browsing/extension_telemetry/extension_telemetry_service.h"

 ... 
```
### patch
```cpp
#include "chrome/browser/profiles/profile_selections.h"

```

### match
```cpp
...
 
 namespace safe_browsing { ... 
 
 bool ExtensionTelemetryServiceFactory::ServiceIsNULLWhileTesting() const { ... 
return true;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
// static
ExtensionTelemetryService* ExtensionTelemetryServiceFactory::GetForProfile(
    Profile* profile) {
  return nullptr;
}

// static
ExtensionTelemetryServiceFactory*
ExtensionTelemetryServiceFactory::GetInstance() {
  static base::NoDestructor<ExtensionTelemetryServiceFactory> instance;
  return instance.get();
}

ExtensionTelemetryServiceFactory::ExtensionTelemetryServiceFactory()
    : ProfileKeyedServiceFactory("ExtensionTelemetryService",
                                 ProfileSelections::BuildNoProfilesSelected()) {
}

bool ExtensionTelemetryServiceFactory::ServiceIsCreatedWithBrowserContext()
    const {
  return false;
}

bool ExtensionTelemetryServiceFactory::ServiceIsNULLWhileTesting() const {
  return true;
}

std::unique_ptr<KeyedService>
ExtensionTelemetryServiceFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const {
  return nullptr;
}

```

