### match
```cpp
...
 
 # ifndef ... 
 
 namespace assist_ranker { ... 
 
 class RankerURLFetcher { ... 
// Returns false if the previous request is not finished, or the request
 // is omitted due to retry limitation. 
 >>> 
bool Request(const GURL& url,
               Callback callback,
               network::mojom::URLLoaderFactory* url_loader_factory);
 ... } ...  } ...  
```
### patch
```cpp
  bool Request_ChromiumImpl(const GURL& url, Callback callback,                    
                       network::mojom::URLLoaderFactory* url_loader_factory);

```

