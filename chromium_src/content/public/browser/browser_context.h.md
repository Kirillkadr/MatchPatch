### match
```cpp
...
 
 # ifndef ... 
#include <stddef.h>

 #include <stdint.h>
 
 >>> 
#include <memory>

 ...
```
### patch
```cpp
#include <optional>

```

### match
```cpp
...
 >>> 
#include "base/functional/function_ref.h"

 ...
```
### patch
```cpp
#include <string>
#include "components/services/storage/public/mojom/blob_storage_context.mojom.h"
#include "content/common/content_export.h"
#include "mojo/public/cpp/bindings/pending_receiver.h"

```

### match
```cpp
...
 >>> 
namespace content {
...
}
 ...
```
### patch
```cpp
namespace content {
class WebContents;
class SessionStorageNamespace;
class StoragePartition;

CONTENT_EXPORT mojo::PendingRemote<storage::mojom::BlobStorageContext>
GetRemoteBlobStorageContextFor(BrowserContext* browser_context);

CONTENT_EXPORT scoped_refptr<content::SessionStorageNamespace>
CreateSessionStorageNamespace(
    content::StoragePartition* partition,
    const std::string& namespace_id,
    std::optional<std::string> clone_from_namespace_id);

CONTENT_EXPORT std::string GetSessionStorageNamespaceId(WebContents*);

}  // namespace content

```

### match
```cpp
...
 >>> 
virtual bool IsOffTheRecord() = 0;
 ...
```
### patch
```cpp
  virtual bool IsTor() const;
  virtual bool IsAIChatAgent() const;

```

