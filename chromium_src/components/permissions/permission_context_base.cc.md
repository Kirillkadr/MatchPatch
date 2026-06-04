### match
```cpp
...
#include <utility>

 #include <variant>
 
 >>> 
#include "base/functional/bind.h"

 ... 
```
### patch
```cpp
#include "base/check.h"
#include "brave/components/brave_wallet/common/buildflags/buildflags.h"
#include "brave/components/permissions/permission_lifetime_manager.h"
#include "components/permissions/permissions_client.h"

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 namespace { ... 
void LogPermissionBlockedMessage(content::RenderFrameHost* rfh,
                                 std::string_view reason,
                                 ContentSettingsType type) {
  rfh->GetOutermostMainFrame()->AddMessageToConsole(
      blink::mojom::ConsoleMessageLevel::kWarning,
      base::StrCat({PermissionUtil::GetPermissionString(type),
                    " permission has been blocked", reason}));
}
 } 
 // namespace 
 >>> 
// static
 ... } ...  
```
### patch
```cpp
#define PermissionContextBase PermissionContextBase_ChromiumImpl

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 bool PermissionContextBase::IsPermissionAvailableToOrigins(
    const GURL& requesting_origin,
    const GURL& embedding_origin) const { ...   >>> 
 if 
 ( 
 !PermissionsClient::Get()->CanBypassEmbeddingOriginCheck(
            requesting_origin, embedding_origin) 
 &&  <<< 
!network::IsUrlPotentiallyTrustworthy(embedding_origin)
 ... ) ...  } ...  } ...  
```
### patch
```cpp
    if (!PermissionsClient::Get()->BraveCanBypassEmbeddingOriginCheck(
            requesting_origin, embedding_origin, content_settings_type_) &&

```

### match
```cpp
...
>>>
 DCHECK 
 ( 
 PermissionsClient::Get()->CanBypassEmbeddingOriginCheck(
             request_data->requesting_origin, request_data->embedding_origin) 
 ||  <<< 
request_data->requesting_origin == request_data->embedding_origin
 ... ) ...  
```
### patch
```cpp
  DCHECK(PermissionsClient::Get()->BraveCanBypassEmbeddingOriginCheck(
             request_data->requesting_origin, request_data->embedding_origin, content_settings_type_) ||

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 void PermissionContextBase::NotifyObservers(
    const ContentSettingsPattern& primary_pattern,
    const ContentSettingsPattern& secondary_pattern,
    ContentSettingsTypeSet content_type_set) const { ... 
for (permissions::Observer& obs : permission_observers_) {
    obs.OnPermissionChanged(primary_pattern, secondary_pattern,
                            content_type_set);
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
#undef PermissionContextBase
PermissionContextBase::PermissionContextBase(
    content::BrowserContext* browser_context,
    ContentSettingsType content_settings_type,
    network::mojom::PermissionsPolicyFeature permissions_policy_feature)
    : PermissionContextBase_ChromiumImpl(browser_context,
                                         content_settings_type,
                                         permissions_policy_feature) {}
PermissionContextBase::~PermissionContextBase() = default;

void PermissionContextBase::SetPermissionLifetimeManagerFactory(
    const base::RepeatingCallback<
        PermissionLifetimeManager*(content::BrowserContext*)>& factory) {
  permission_lifetime_manager_factory_ = factory;
}

void PermissionContextBase::PermissionDecided(
    PermissionDecision decision,
    bool is_final_decision,
    const PermissionRequestData& request_data) {
  if (permission_lifetime_manager_factory_) {
    const auto request_it = pending_requests_.find(request_data.id.ToString());
    if (request_it != pending_requests_.end()) {
      const PermissionRequest* permission_request =
          request_it->second.first.get();
      CHECK(permission_request);
      if (auto* permission_lifetime_manager =
              permission_lifetime_manager_factory_.Run(browser_context_)) {
        permission_lifetime_manager->PermissionDecided(
            *permission_request, request_data.requesting_origin,
            request_data.embedding_origin, decision);
      }
    }
  }

  PermissionContextBase_ChromiumImpl::PermissionDecided(
      decision, is_final_decision, request_data);
}

```

