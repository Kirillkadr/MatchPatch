### match
```cpp
...
 
std::optional<url::Origin> GetAutoApprovalOrigin(
      content::BrowserContext* browser_context) override;
  std::optional<permissions::PermissionAction> GetAutoApprovalStatus(
      content::BrowserContext* browser_context,
      const GURL& origin) override; 
 >>> 
...
```
### patch
```cpp
bool BraveCanBypassEmbeddingOriginCheck(const GURL& requesting_origin,
                                     const GURL& embedding_origin,
                                     ContentSettingsType type) override;

```

### match
```cpp
...
 
 class ChromePermissionsClient : public permissions::PermissionsClient { ... 
 
 #if BUILDFLAG(IS_ANDROID ) ... 
 const url::Origin& origin 
 ) 
 override 
 ; 
 >>> 
 ... } ...  
```
### patch
```cpp
  std::unique_ptr<PermissionMessageDelegate> MaybeCreateMessageUI_ChromiumImpl(
      content::WebContents* web_contents, ContentSettingsType type,
      base::WeakPtr<permissions::PermissionPromptAndroid> prompt);

```

