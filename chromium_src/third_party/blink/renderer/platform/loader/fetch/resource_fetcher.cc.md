### match
```
...
#include <string_view>

 #include <utility>
 
 >>> 
#include "base/auto_reset.h"

 ... 
```
### patch
```
#include "third_party/blink/public/common/features.h"
#include "third_party/blink/renderer/platform/loader/fetch/memory_cache.h"

```

### match
```
...
 namespace blink { ... 
 String ResourceFetcher::GetCacheIdentifier(const KURL& url,
                                           bool skip_service_worker) const { ... 
if (bundle) {
    return bundle->GetCacheIdentifier();
  }  >>> 
 return MemoryCache::DefaultCacheIdentifier();  <<< ... } ...  } ...  
```
### patch
```
  return MemoryCache::DefaultCacheIdentifier().empty() ? GetContextCacheIdentifier()
                                   : GetContextCacheIdentifier();

```

### match
```
...
 namespace blink { ... 
 void ResourceFetcher::ResourcePrepareHelper::RecordTrace() { ... 
TRACE_EVENT_INSTANT(TRACE_DISABLED_BY_DEFAULT("network"),
                      "ResourcePrioritySet",
                      perfetto::Track(resource_request.InspectorId()),
                      "priority", resource_request.Priority());
 } 
 >>> 
 ... } ...  
```
### patch
```
// This method returns a custom cache identifier for a Context to be used in
// blink::MemoryCache to properly partition requests from third-party frames
// when already existing entries in blink::MemoryCache should not be used.
String ResourceFetcher::GetContextCacheIdentifier() const {
  if (!base::FeatureList::IsEnabled(features::kPartitionBlinkMemoryCache)) {
    return MemoryCache::DefaultCacheIdentifier();
  }
  if (!properties_->IsOutermostMainFrame()) {
    if (auto cache_identifier =
            Context().GetCacheIdentifierIfCrossSiteSubframe()) {
      return cache_identifier;
    }
  }
  return MemoryCache::DefaultCacheIdentifier();
}

```

