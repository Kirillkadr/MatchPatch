### match
```
...
#include "third_party/blink/renderer/platform/heap/garbage_collected.h"

 #include "third_party/blink/renderer/platform/wtf/functional.h"
 
 >>> 
using device::mojom::blink::UsbClaimInterfaceResult;
 ... 
```
### patch
```
#include "brave/third_party/blink/renderer/brave_farbling_constants.h"
#include "brave/third_party/blink/renderer/core/farbling/brave_session_cache.h"
#include "third_party/blink/renderer/platform/wtf/text/string_builder.h"

```

### match
```
...
 namespace blink { ... 
 void USBDevice::MarkRequestComplete(ScriptPromiseResolverBase* resolver) { ... 
device_requests_.erase(request_entry);
 } 
 >>> 
 ... } ...  
```
### patch
```
String USBDevice::serialNumber() const {
  String realSerialNumber = serialNumber_ChromiumImpl();
  if (realSerialNumber.length() > 0) {
    if (ExecutionContext* context = GetExecutionContext()) {
      if (brave::GetBraveFarblingLevelFor(
              context,
              ContentSettingsType::BRAVE_WEBCOMPAT_USB_DEVICE_SERIAL_NUMBER,
              BraveFarblingLevel::BALANCED) != BraveFarblingLevel::OFF) {
        StringBuilder result;
        result.Append(realSerialNumber);
        result.Append("WEBUSB_SERIAL_NUMBER");
        return brave::BraveSessionCache::From(*context).GenerateRandomString(
            result.ToString().Utf8(), 16);
      }
    }
  }
  return realSerialNumber;
}

```

