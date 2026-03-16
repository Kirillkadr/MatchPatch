### match
```
...
 # ifndef ... 
 class BitmapFetcherService : public KeyedService, public BitmapFetcherDelegate { ... 
// NOTE: The callback might be called back synchronously from RequestImage if
 // the image is already in the cache. 
 >>> 
RequestId RequestImage(const GURL& url, BitmapFetchedCallback callback);
 ... } ...  
```
### patch
```
  RequestId RequestImageWithNetworkTrafficAnnotationTag(
      const GURL& url, BitmapFetchedCallback callback,
      const net::NetworkTrafficAnnotationTag& traffic_annotation); 

```

