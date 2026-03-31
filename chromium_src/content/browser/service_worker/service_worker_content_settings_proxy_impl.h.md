### match
```cpp
...
 
 # ifndef ... 
#include "third_party/blink/public/mojom/worker/worker_content_settings_proxy.mojom.h"

 #include "url/origin.h"
 
 >>> 
namespace content {

class ServiceWorkerContextWrapper;

// ServiceWorkerContentSettingsProxyImpl passes content settings to its renderer
// counterpart blink::ServiceWorkerContentSettingsProxy
// Created on EmbeddedWorkerInstance::SendStartWorker() and connects to the
// counterpart at the moment.
// EmbeddedWorkerInstance owns this class, so the lifetime of this class is
// strongly associated to it. This class lives on the UI thread.
class ServiceWorkerContentSettingsProxyImpl final
    : public blink::mojom::WorkerContentSettingsProxy {
 public:
  ServiceWorkerContentSettingsProxyImpl(
      const GURL& script_url,
      scoped_refptr<ServiceWorkerContextWrapper> context_wrapper,
      mojo::PendingReceiver<blink::mojom::WorkerContentSettingsProxy> receiver,
      blink::StorageKey storage_key);

  ~ServiceWorkerContentSettingsProxyImpl() override;

  // blink::mojom::WorkerContentSettingsProxy implementation
  void AllowIndexedDB(AllowIndexedDBCallback callback) override;
  void AllowCacheStorage(AllowCacheStorageCallback callback) override;
  void AllowWebLocks(AllowCacheStorageCallback callback) override;
  void RequestFileSystemAccessSync(
      RequestFileSystemAccessSyncCallback callback) override;

 private:
  const url::Origin origin_;
  scoped_refptr<ServiceWorkerContextWrapper> context_wrapper_;
  mojo::Receiver<blink::mojom::WorkerContentSettingsProxy> receiver_;
  const blink::StorageKey storage_key_;
};

}
 ... 
```
### patch
```cpp
// We explicitly include ancestor class here so our function redeclaration only
// affects this class.
#include "third_party/blink/public/mojom/worker/worker_content_settings_proxy.mojom.h"

```

### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
void AllowCacheStorage(AllowCacheStorageCallback callback) override;
 void AllowWebLocks(AllowCacheStorageCallback callback) override; 
 >>> 
void RequestFileSystemAccessSync(
      RequestFileSystemAccessSyncCallback callback) override;
 ... } ...  
```
### patch
```cpp
  void GetBraveShieldsSettings(GetBraveShieldsSettingsCallback callback) override; 

```

