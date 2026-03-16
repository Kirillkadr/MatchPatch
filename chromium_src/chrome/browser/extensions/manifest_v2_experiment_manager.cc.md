### match
```
...
#include "base/strings/stringprintf.h"

 #include "base/types/pass_key.h"
 
 >>> 
#include "chrome/browser/extensions/chrome_extension_system_factory.h"

 ...
```
### patch
```
#include "brave/browser/extensions/manifest_v2/features.h"

```

### match
```
...
#include "services/metrics/public/cpp/ukm_recorder.h"

 static_assert(BUILDFLAG(ENABLE_EXTENSIONS_CORE)); 
 >>> 
namespace extensions {
...
}
 ...
```
### patch
```
namespace {

extensions::MV2ExperimentStage AdjustMV2ExperimentStage(
    extensions::MV2ExperimentStage experiment_stage) {
  if (!base::FeatureList::IsEnabled(
          extensions_mv2::features::kExtensionsManifestV2)) {
    return experiment_stage;
  }
  // We relax any stage into the Warning stage.
  return extensions::MV2ExperimentStage::kWarning;
}

}  // namespace


```

### match
```
...
 
 namespace extensions { ... 
   >>> 
 : 
 experiment_stage_(CalculateCurrentExperimentStage()) 
 ,  <<< 
// Note: passing `ExtensionManagement` is safe and guaranteed to outlive
 ... } ...
```
### patch
```
      experiment_stage_(AdjustMV2ExperimentStage(CalculateCurrentExperimentStage())),

```

