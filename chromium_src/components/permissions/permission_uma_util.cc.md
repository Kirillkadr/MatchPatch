### match
```cpp
...
#include <utility>

 #include <variant>
 
 >>> 
#include "base/check_op.h"

 ... 
```
### patch
```cpp
#include "components/permissions/permissions_client.h"

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 namespace { ... 
 
 std::string GetPermissionStringForUma(
    ContentSettingsType content_setting_type) { ... 
 default 
 : 
 >>> 
break;
 ... } ...  } ...  } ...  
```
### patch
```cpp
      return "";

```

### match
```cpp
...
 
 namespace permissions { ... 
 void PermissionUmaUtil::RecordPermissionUsage ( ... 
 const GURL& requesting_origin 
 ) 
 { 
 >>> 
PermissionsClient::Get()->GetUkmSourceId(
      permission_type, browser_context, render_frame_host, requesting_origin,
      base::BindOnce(&RecordPermissionUsageUkm, permission_type));
 ... } ...  } ...  
```
### patch
```cpp
  PermissionsClient::Get()->GetSettingsMap(browser_context); \
  if (true)                        \
    return;                        \

```

### match
```cpp
...
 
 namespace permissions { ... 
 void PermissionUmaUtil::RecordPermissionUsageNotificationShown ( ... 
 uint64_t site_engagement_level 
 ) 
 { 
 >>> 
PermissionsClient::Get()->GetUkmSourceId(
      ContentSettingsType::NOTIFICATIONS, browser_context, nullptr,
      requesting_origin,
      base::BindOnce(&RecordPermissionUsageNotificationShownUkm,
                     did_user_always_allow_notifications, is_allowlisted,
                     suspicious_score, site_engagement_level));
 ... } ...  } ...  
```
### patch
```cpp
  PermissionsClient::Get()->GetSettingsMap(browser_context); \
  if (true)                        \
    return;                        \

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 void PermissionUmaUtil::RecordPermissionAction(
    ContentSettingsType permission,
    PermissionAction action,
    PermissionSourceUI source_ui,
    PermissionRequestGestureType gesture_type,
    base::TimeDelta time_to_action,
    PermissionPromptDisposition ui_disposition,
    std::optional<PermissionPromptDispositionReason> ui_reason,
    std::optional<std::vector<ElementAnchoredBubbleVariant>> variants,
    const GURL& requesting_origin,
    content::BrowserContext* browser_context,
    content::RenderFrameHost* render_frame_host,
    std::optional<PermissionUiSelector::PredictionGrantLikelihood>
        predicted_grant_likelihood,
    std::optional<PermissionRequestRelevance> permission_request_relevance,
    std::optional<permissions::PermissionAiRelevanceModel>
        permission_ai_relevance_model,
    std::optional<bool> prediction_decision_held_back,
    const PromptOptions& prompt_options,
    std::optional<GeolocationAccuracy> initial_geolocation_accuracy_selection,
    std::optional<ukm::SourceId> source_id) { ... 
 
 if (source_id.has_value() && source_id.value() != ukm::kInvalidSourceId) { ... 
RecordPermissionActionUkm(std::move(params), source_id);
 } 
 else 
 { 
 >>> 
PermissionsClient::Get()->GetUkmSourceId(
        permission, browser_context, render_frame_host, requesting_origin,
        base::BindOnce(&RecordPermissionActionUkm, std::move(params)));
 ... } ...  } ...  } ...  
```
### patch
```cpp
    PermissionsClient::Get()->GetSettingsMap(browser_context); \
  if (true)                        \
    return;                        \

```

### match
```cpp
...
 
 namespace permissions { ... 
 
 void PermissionUmaUtil::RecordElementAnchoredPermissionPromptAction(
    const std::vector<std::unique_ptr<PermissionRequest>>& requests,
    const std::vector<base::WeakPtr<permissions::PermissionRequest>>&
        screen_requests,
    ElementAnchoredBubbleAction action,
    ElementAnchoredBubbleVariant variant,
    int screen_counter,
    const GURL& requesting_origin,
    content::BrowserContext* browser_context) { ... 
 RequestTypeToContentSettingsType(requests[0]->request_type()) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  PermissionsClient::Get()->GetSettingsMap(browser_context); \
  if (true)                        \
    return;                        \

```

