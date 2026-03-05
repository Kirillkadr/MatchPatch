### match
```
...
 # ifndef ... 
#define THIRD_PARTY_BLINK_RENDERER_CORE_LOADER_MIXED_CONTENT_CHECKER_H_

 #include <optional>
 
 >>> 
#include "base/gtest_prod_util.h"

 ... 
```
### patch
```
// We are hiding IsMixedContent(const String& origin_protocol, const KURL&)
// because we want to enforce mixed content checks on .onion origins.
// Publicly available protocol-only overload of this method allows to skip
// .onion specific checks which we don't want.

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class CORE_EXPORT MixedContentChecker final { ... 
// |execution_context_for_logging| is used only for logging, use counters,
 // UKM-related things. 
 >>> 
static void UpgradeInsecureRequest(
      ResourceRequest&,
      const FetchClientSettingsObject* fetch_client_settings_object,
      ExecutionContext* execution_context_for_logging,
      mojom::RequestContextFrameType,
      WebContentSettingsClient* settings_client,
      LocalFrame* frame);
 ... } ...  } ...  
```
### patch
```

 private:
  static bool IsMixedContent(const String& origin_protocol, const KURL&);
  static std::optional<bool> IsMixedContentForOnion(const SecurityOrigin*,
                                                    const KURL& url);

 public:

```

### match
```
...
 static 
 void 
 UpgradeInsecureRequest 
 ( 
 >>> 
ResourceRequest&
 ... ) ...  
```
### patch
```
      ResourceRequest&,
      const FetchClientSettingsObject* fetch_client_settings_object,
      ExecutionContext* execution_context_for_logging,
      mojom::RequestContextFrameType,
      WebContentSettingsClient* settings_client, LocalFrame* frame);       
  static void UpgradeInsecureRequest_ChromiumImpl(

```

