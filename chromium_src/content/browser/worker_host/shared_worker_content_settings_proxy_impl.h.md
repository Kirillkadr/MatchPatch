### match
```cpp
...
 
 # ifndef ... 
#include "third_party/blink/public/mojom/worker/worker_content_settings_proxy.mojom.h"

 #include "url/origin.h"
 
 >>> 
namespace content {

class SharedWorkerHost;

// SharedWorkerContentSettingsProxyImpl passes content settings to its renderer
// counterpart blink::SharedWorkerContentSettingsProxy.
// Created on SharedWorker::Start() and connects to the counterpart
// at the moment.
// SharedWorkerHost owns this class, so the lifetime of this class is strongly
// associated to it.
class SharedWorkerContentSettingsProxyImpl
    : public blink::mojom::WorkerContentSettingsProxy {
 public:
  SharedWorkerContentSettingsProxyImpl(
      const GURL& script_url,
      SharedWorkerHost* owner,
      mojo::PendingReceiver<blink::mojom::WorkerContentSettingsProxy> receiver);

  SharedWorkerContentSettingsProxyImpl(
      const SharedWorkerContentSettingsProxyImpl&) = delete;
  SharedWorkerContentSettingsProxyImpl& operator=(
      const SharedWorkerContentSettingsProxyImpl&) = delete;

  ~SharedWorkerContentSettingsProxyImpl() override;

  // blink::mojom::WorkerContentSettingsProxy implementation.
  void AllowIndexedDB(AllowIndexedDBCallback callback) override;
  void AllowCacheStorage(AllowCacheStorageCallback callback) override;
  void AllowWebLocks(AllowCacheStorageCallback callback) override;
  void RequestFileSystemAccessSync(
      RequestFileSystemAccessSyncCallback callback) override;

 private:
  const url::Origin origin_;
  raw_ptr<SharedWorkerHost> owner_;
  mojo::Receiver<blink::mojom::WorkerContentSettingsProxy> receiver_;
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

