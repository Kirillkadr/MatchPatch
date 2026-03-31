### match
```cpp
...
// found in the LICENSE file.
 #include "chrome/browser/permissions/permission_manager_factory.h"
 
 >>> 
#include "build/build_config.h"

 ... 
```
### patch
```cpp
#include "brave/browser/geolocation/brave_geolocation_permission_context_delegate.h"
#include "brave/browser/permissions/permission_lifetime_manager_factory.h"
#include "brave/components/brave_wallet/common/buildflags/buildflags.h"
#include "brave/components/permissions/contexts/brave_google_sign_in_permission_context.h"
#include "brave/components/permissions/contexts/brave_open_ai_chat_permission_context.h"
#include "brave/components/permissions/permission_lifetime_manager.h"

```

### match
```cpp
...
#include "components/permissions/contexts/web_app_installation_permission_context.h"

 #include "components/permissions/contexts/window_management_permission_context.h"
 
 >>> 
#include "components/permissions/permission_manager.h"

 ... 
```
### patch
```cpp
#include "components/permissions/features.h"

```

### match
```cpp
...
#include "components/permissions/permission_manager.h"

 #include "extensions/buildflags/buildflags.h"
 
 >>> 
#if BUILDFLAG(ENABLE_EXTENSIONS)
#include "chrome/browser/clipboard/chrome_clipboard_permission_context_delegate.h"
#endif
 ... 
```
### patch
```cpp
#if BUILDFLAG(ENABLE_BRAVE_WALLET)
#include "brave/components/permissions/contexts/brave_wallet_permission_context.h"
#endif


```

### match
```cpp
...
 
 namespace { ... 
 
 permissions::PermissionManager::PermissionContextMap CreatePermissionContexts(
    Profile* profile) { ... 
 
 # else ...   >>> 
 std::make_unique<GeolocationPermissionContextDelegate>(profile) 
 ;  <<<  ...} ...  } ...  
```
### patch
```cpp
      std::make_unique<BraveGeolocationPermissionContextDelegate>(profile);

```

### match
```cpp
...
 std::unique_ptr<KeyedService>
  >>> 
 PermissionManagerFactory::BuildServiceInstanceForBrowserContext 
 (  <<< 
content::BrowserContext* context
 ... ) ...  
```
### patch
```cpp
PermissionManagerFactory::BuildServiceInstanceForBrowserContext_ChromiumImpl(

```

### match
```cpp
...
 
 std::unique_ptr<KeyedService>
PermissionManagerFactory::BuildServiceInstanceForBrowserContext_ChromiumImpl(
content::BrowserContext* context) const { ... 
return std::make_unique<permissions::PermissionManager>(
      profile, CreatePermissionContexts(profile));
 } 
 >>> 
 ... 
```
### patch
```cpp
std::unique_ptr<KeyedService>
PermissionManagerFactory::BuildServiceInstanceForBrowserContext(
    content::BrowserContext* context) const {
  Profile* profile = Profile::FromBrowserContext(context);
  auto permission_contexts = CreatePermissionContexts(profile);

#if BUILDFLAG(ENABLE_BRAVE_WALLET)
  permission_contexts[ContentSettingsType::BRAVE_ETHEREUM] =
      std::make_unique<permissions::BraveWalletPermissionContext>(
          profile, ContentSettingsType::BRAVE_ETHEREUM);
  permission_contexts[ContentSettingsType::BRAVE_SOLANA] =
      std::make_unique<permissions::BraveWalletPermissionContext>(
          profile, ContentSettingsType::BRAVE_SOLANA);
  permission_contexts[ContentSettingsType::BRAVE_CARDANO] =
      std::make_unique<permissions::BraveWalletPermissionContext>(
          profile, ContentSettingsType::BRAVE_CARDANO);
#endif
  permission_contexts[ContentSettingsType::BRAVE_GOOGLE_SIGN_IN] =
      std::make_unique<permissions::BraveGoogleSignInPermissionContext>(
          profile);
  permission_contexts[ContentSettingsType::BRAVE_OPEN_AI_CHAT] =
      std::make_unique<permissions::BraveOpenAIChatPermissionContext>(profile);

  if (base::FeatureList::IsEnabled(
          permissions::features::kPermissionLifetime)) {
    auto factory =
        base::BindRepeating(&PermissionLifetimeManagerFactory::GetForProfile);
    for (auto& permission_context : permission_contexts) {
      permission_context.second->SetPermissionLifetimeManagerFactory(factory);
    }
  }

  return std::make_unique<permissions::PermissionManager>(
      profile, std::move(permission_contexts));
}
```

