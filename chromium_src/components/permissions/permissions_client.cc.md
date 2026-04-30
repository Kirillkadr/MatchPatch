### match
```cpp
...
 
 namespace permissions { ... 
 
 favicon::FaviconService* PermissionsClient::GetFaviconService(
    content::BrowserContext* browser_context) { ... 
return nullptr;
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool PermissionsClient::BraveCanBypassEmbeddingOriginCheck(
    const GURL& requesting_origin,
    const GURL& embedding_origin,
    ContentSettingsType type) {
  return CanBypassEmbeddingOriginCheck(requesting_origin, embedding_origin);
}

```

