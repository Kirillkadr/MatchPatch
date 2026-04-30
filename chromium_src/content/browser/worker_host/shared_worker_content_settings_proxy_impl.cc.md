### match
```cpp
...
 
 namespace content { ... 
 
 void SharedWorkerContentSettingsProxyImpl::RequestFileSystemAccessSync(
    RequestFileSystemAccessSyncCallback callback) { ... 
if (!origin_.opaque()) {
    owner_->AllowFileSystem(origin_.GetURL(), std::move(callback));
  } else {
    std::move(callback).Run(false);
  }
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void SharedWorkerContentSettingsProxyImpl::GetBraveShieldsSettings(
    GetBraveShieldsSettingsCallback callback) {
  // Shields should also work in opaque origins.
  const GURL url = origin_.GetTupleOrPrecursorTupleIfOpaque().GetURL();
  owner_->GetBraveShieldsSettings(url, std::move(callback));
}

```

