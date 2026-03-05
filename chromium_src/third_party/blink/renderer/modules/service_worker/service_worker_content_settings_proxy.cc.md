### match
```
...
#include "third_party/blink/renderer/modules/service_worker/service_worker_content_settings_proxy.h"

 #include <memory>
 
 >>> 
#include "base/metrics/histogram_macros.h"

 ... 
```
### patch
```
#include "base/check.h"
#include "brave/components/brave_shields/core/common/shields_settings.mojom-blink.h"
#include "mojo/public/cpp/bindings/string_traits_wtf.h"

```

### match
```
...
 namespace blink { ... 
 mojo::Remote<mojom::blink::WorkerContentSettingsProxy>&
ServiceWorkerContentSettingsProxy::GetService() { ... 
return *content_settings_instance_host;
 } 
 >>> 
 ... } ...  
```
### patch
```
brave_shields::mojom::ShieldsSettingsPtr
ServiceWorkerContentSettingsProxy::GetBraveShieldsSettings(
    ContentSettingsType webcompat_settings_type) {
  brave_shields::mojom::blink::ShieldsSettingsPtr blink_result;
  if (!GetService()->GetBraveShieldsSettings(&blink_result)) {
    return brave_shields::mojom::ShieldsSettings::New();
  }
  // Convert the blink mojo struct into a non-blink mojo struct.
  CHECK(blink_result);
  brave_shields::mojom::ShieldsSettingsPtr result;
  CHECK(brave_shields::mojom::ShieldsSettings::DeserializeFromMessage(
      brave_shields::mojom::blink::ShieldsSettings::WrapAsMessage(
          std::move(blink_result)),
      &result));
  return result;
}

```

