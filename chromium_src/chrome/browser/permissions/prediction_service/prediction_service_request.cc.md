### match
```cpp
...
#include "base/functional/bind.h"

 #include "base/functional/callback_helpers.h"
 
 >>> 
#include "components/permissions/prediction_service/prediction_service.h"

 ... 
```
### patch
```cpp
#include "base/task/sequenced_task_runner.h"

```

### match
```cpp
...
 
 void PredictionServiceRequest::LookupResponseReceived(
    bool lookup_succesful,
    bool response_from_cache,
    const std::optional<permissions::GeneratePredictionsResponse>& response) { ... 
std::move(callback_).Run(lookup_succesful, response_from_cache, response);
 } 
 >>> 
 ... 
```
### patch
```cpp
PredictionServiceRequest::PredictionServiceRequest(
    permissions::PredictionService* service,
    const permissions::PredictionRequestFeatures& entity,
    permissions::PredictionServiceBase::LookupResponseCallback callback)
    : callback_(std::move(callback)) {
  // Fail the prediction service request
  base::SequencedTaskRunner::GetCurrentDefault()->PostTask(
      FROM_HERE,
      base::BindOnce(&PredictionServiceRequest::LookupResponseReceived,
                     weak_factory_.GetWeakPtr(), false, false, std::nullopt));
}

PredictionServiceRequest::~PredictionServiceRequest() = default;

void PredictionServiceRequest::LookupResponseReceived(
    bool lookup_succesful,
    bool response_from_cache,
    const std::optional<permissions::GeneratePredictionsResponse>& response) {
  std::move(callback_).Run(lookup_succesful, response_from_cache, response);
}
```

