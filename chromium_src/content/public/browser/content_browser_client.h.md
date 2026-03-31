### match
```cpp
...
 >>> 
virtual void SetBrowserStartupIsCompleteForTesting();
 ...
```
### patch
```cpp
  virtual void MaybeHideReferrer(
      BrowserContext* browser_context, const GURL& request_url,
      const GURL& document_url, blink::mojom::ReferrerPtr* referrer) {}
  virtual std::string GetEffectiveUserAgent(BrowserContext* browser_context,
                                            const GURL& url);
  virtual std::optional<base::UnguessableToken> GetEphemeralStorageToken(
      RenderFrameHost* render_frame_host, const url::Origin& origin);
  virtual bool AllowWorkerFingerprinting(const GURL& url,
                                         BrowserContext* browser_context);
  virtual brave_shields::mojom::ShieldsSettingsPtr
  WorkerGetBraveShieldSettings(const GURL& url,
                               BrowserContext* browser_context);
  virtual std::optional<GURL> SanitizeURL(content::RenderFrameHost*,
                                          const GURL&);
  virtual bool IsWindowsRecallDisabled();
  virtual bool ShouldInheritStoragePartition(
      const content::StoragePartitionConfig& partition_config) const;

```

