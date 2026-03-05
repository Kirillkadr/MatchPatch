### match
```
...
 # ifndef ... 
 #define THIRD_PARTY_BLINK_RENDERER_MODULES_SERVICE_WORKER_SERVICE_WORKER_CONTENT_SETTINGS_PROXY_H_
 
 >>> 
#include "mojo/public/cpp/bindings/pending_remote.h"

 ... 
```
### patch
```
#include "brave/third_party/blink/renderer/brave_farbling_constants.h"
#include "third_party/blink/public/platform/web_content_settings_client.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class ServiceWorkerContentSettingsProxy final
    : public blink::WebContentSettingsClient { ... 
// Asks the browser process about the settings.
 // Blocks until the response arrives. 
 >>> 
bool AllowStorageAccessSync(StorageType storage_type) override;
 ... } ...  } ...  
```
### patch
```
  bool UnusedFunction() {                                                
    return false;
  }
  brave_shields::mojom::ShieldsSettingsPtr GetBraveShieldsSettings(
      ContentSettingsType webcompat_settings_type) override;

```

