### match
```cpp
...
 
 # ifndef ... 
 
 class HttpsUpgradesInterceptor : public content::URLLoaderRequestInterceptor,
                                 public network::mojom::URLLoader { ... 
HttpsUpgradesInterceptor& operator=(const HttpsUpgradesInterceptor&) = delete;
 // content::URLLoaderRequestInterceptor: 
 >>> 
void MaybeCreateLoader(
      const network::ResourceRequest& tentative_resource_request,
      content::BrowserContext* browser_context,
      content::URLLoaderRequestInterceptor::LoaderCallback callback) override;
 ... } ...  
```
### patch
```cpp
  void  MaybeCreateLoader_ChromiumImpl(
      const network::ResourceRequest& tentative_resource_request,
      content::BrowserContext* browser_context,
      content::URLLoaderRequestInterceptor::LoaderCallback callback);

```

