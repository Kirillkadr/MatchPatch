### match
```
...
 # ifndef ... 
// content_settings::ContentSettingsManagerImpl::Delegate:  >>> 
 scoped_refptr<content_settings::CookieSettings> GetCookieSettings(
      content::BrowserContext* browser_context) override;  <<< ... 
bool AllowStorageAccess(
      const content::GlobalRenderFrameHostToken& frame_token,
      content_settings::mojom::ContentSettingsManager::StorageType storage_type,
      const GURL& url,
      bool allowed,
      base::OnceCallback<void(bool)>* callback) override;
 ... 
```
### patch
```
  scoped_refptr<content_settings::CookieSettings> GetCookieSettings(content::BrowserContext* browser_context) override;                    \
  void GetBraveShieldsSettings(
      const content::GlobalRenderFrameHostToken& frame_token,
      content_settings::mojom::ContentSettingsManager::       
          GetBraveShieldsSettingsCallback callback) override;

```

