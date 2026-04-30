### match
```cpp
...
 
 # ifndef ... 
 #define COMPONENTS_CONTENT_SETTINGS_BROWSER_CONTENT_SETTINGS_MANAGER_IMPL_H_
 
 >>> 
#include "base/memory/scoped_refptr.h"

 ... 
```
### patch
```cpp
#include "base/containers/flat_map.h"
#include "brave/components/brave_shields/core/common/shields_settings.mojom.h"
#include "components/content_settings/common/content_settings_manager.mojom.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 class ContentSettingsManagerImpl
    : public content_settings::mojom::ContentSettingsManager { ... 
 
 class Delegate { ... 
 content::BrowserContext* browser_context 
 ) 
 = 
 0 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  virtual void GetBraveShieldsSettings(
      const content::GlobalRenderFrameHostToken& frame_token,
      GetBraveShieldsSettingsCallback callback) = 0;

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content_settings { ... 
 
 class ContentSettingsManagerImpl
    : public content_settings::mojom::ContentSettingsManager { ... 
 base::OnceCallback<void(bool)> callback 
 ) 
 override 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void AllowEphemeralStorageAccess(
      const blink::LocalFrameToken& frame_token, const url::Origin& origin,
      const net::SiteForCookies& site_for_cookies,
      const url::Origin& top_frame_origin,
      AllowEphemeralStorageAccessCallback callback) override;
  void GetBraveShieldsSettings(const blink::LocalFrameToken& frame_token,
                               GetBraveShieldsSettingsCallback callback)
      override;                                                             

```

