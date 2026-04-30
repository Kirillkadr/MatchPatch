### match
```cpp
...
 
 namespace content { ... 
 
 void ServiceWorkerContentSettingsProxyImpl::RequestFileSystemAccessSync(
    RequestFileSystemAccessSyncCallback callback) { ... 
mojo::ReportBadMessage(
      "The FileSystem API is not exposed to service workers "
      "but somehow a service worker requested access.");
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void ServiceWorkerContentSettingsProxyImpl::GetBraveShieldsSettings(
    GetBraveShieldsSettingsCallback callback) {
  DCHECK_CURRENTLY_ON(BrowserThread::UI);
  // May be shutting down.
  if (!context_wrapper_->browser_context()) {
    std::move(callback).Run(brave_shields::mojom::ShieldsSettings::New());
    return;
  }
  // Shields should also work in opaque origins.
  const GURL url = origin_.GetTupleOrPrecursorTupleIfOpaque().GetURL();
  std::move(callback).Run(
      GetContentClient()->browser()->WorkerGetBraveShieldSettings(
          url, context_wrapper_->browser_context()));
}

```

