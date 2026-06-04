### match
```cpp
...
// found in the LICENSE file.
 #include "components/page_image_service/image_service_consent_helper.h"
 
 >>> 
#include "base/metrics/histogram_functions.h"

 ... 
```
### patch
```cpp
#include "components/sync/service/sync_service_utils.h"

```

### match
```cpp
...
 
 namespace page_image_service { ... 
 
 std::optional<bool> ImageServiceConsentHelper::GetConsentStatus() { ...   >>> 
 if 
 ( 
 syncer::GetUploadToGoogleState(sync_service_, data_type_) 
 ==  <<< 
syncer::UploadState::NOT_ACTIVE
 ... ) ...  } ...  } ...  
```
### patch
```cpp
  if (syncer::RejectConsent() || syncer::GetUploadToGoogleState(sync_service_, data_type_) ==

```

### match
```cpp
...
 
 namespace page_image_service { ... 
void ImageServiceConsentHelper::OnTimeoutExpired() {
  // The request callbacks can modify the vector while running. Swap the vector
  // onto the stack to prevent crashing. https://crbug.com/1472360.
  std::vector<std::pair<base::OnceCallback<void(PageImageServiceConsentStatus)>,
                        mojom::ClientId>>
      callbacks;
  std::swap(callbacks, enqueued_request_callbacks_);
  for (auto& request_callback_with_client_id : callbacks) {
    // Report consent status on timeout for each request to compare against the
    // number of all requests.
    PageImageServiceConsentStatus consent_status =
        ConsentStatusToUmaStatus(GetConsentStatus());
    base::UmaHistogramEnumeration("PageImageService.ConsentStatusOnTimeout",
                                  consent_status);
    std::move(request_callback_with_client_id.first).Run(consent_status);
  }
}
 } 
 // namespace page_image_service 
 >>> 
 ... 
```
### patch
```cpp
namespace syncer {
bool RejectConsent() {
  return true;
}
}  // namespace syncer
```

