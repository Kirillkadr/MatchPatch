### match
```
...
 # ifndef ... 
#include <memory>

 #include <optional>
 
 >>> 
#include "base/types/pass_key.h"

 ... 
```
### patch
```
#include "base/check.h"

```

### match
```
...
 # ifndef ... 
 namespace blink { ... 
 class PLATFORM_EXPORT SecurityOrigin : public RefCounted<SecurityOrigin> { ... 
const base::UnguessableToken& AgentClusterId() const {
    return agent_cluster_id_;
  }
 // Returns true if this security origin is serialized to "null". 
 >>> 
bool SerializesAsNull() const;
 ... } ...  } ...  
```
### patch
```
  static const base::UnguessableToken GetNonceForEphemeralStorageKeying(
      const blink::SecurityOrigin* origin) {
    CHECK(origin->IsOpaque());
    return *origin->GetNonceForSerialization();
  }
  static const base::UnguessableToken GetNonceForEphemeralStorageKeying(
      const scoped_refptr<const blink::SecurityOrigin>& origin) {
    return GetNonceForEphemeralStorageKeying(origin.get());
  }                                                                      

```

