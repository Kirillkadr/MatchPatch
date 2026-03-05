### match
```
...
#include <memory>

 #include <utility>
 
 >>> 
#include "services/network/public/mojom/attribution.mojom-blink.h"

 ... 
```
### patch
```
#include "brave/components/brave_page_graph/common/buildflags.h"
#include "third_party/blink/renderer/core/dom/dom_node_ids.h"
#include "third_party/blink/renderer/core/frame/ad_tracker.h"
#include "third_party/blink/renderer/core/probe/core_probes.h"
#include "third_party/blink/renderer/platform/loader/fetch/fetch_parameters.h"

```

### match
```
...
 namespace blink { ... 
 void ImageLoader::DoUpdateFromElement(const DOMWrapperWorld* world,
                                      UpdateFromElementBehavior update_behavior,
                                      const KURL* source_url,
                                      UpdateType update_type,
                                      bool force_blocking) { ... 
 if (!url.IsNull() && !url.IsEmpty()) { ... 
// <img srcset>.
 ResourceLoaderOptions resource_loader_options(std::move(world)); 
 >>> 
resource_loader_options.initiator_info.name = GetElement()->localName();
 ... } ...  } ...  } ...  
```
### patch
```
    #if BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)
resource_loader_options.initiator_info.dom_node_id =
    CoreProbeSink::HasAgentsGlobal(CoreProbeSink::PageGraph)
        ? DOMNodeIds::IdForNode(GetElement())
        : kInvalidDOMNodeId;
#endif  // BUILDFLAG(ENABLE_BRAVE_PAGE_GRAPH)

```

