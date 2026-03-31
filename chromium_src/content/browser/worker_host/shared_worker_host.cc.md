### match
```cpp
...
 
 namespace content { ... 
 
 void SharedWorkerHost::OnWorkerConnectionLost() { ... 
Destruct();
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
void SharedWorkerHost::GetBraveShieldsSettings(
    const GURL& url,
    base::OnceCallback<void(brave_shields::mojom::ShieldsSettingsPtr)>
        callback) {
  std::move(callback).Run(
      GetContentClient()->browser()->WorkerGetBraveShieldSettings(
          url, GetProcessHost()->GetBrowserContext()));
}

```

