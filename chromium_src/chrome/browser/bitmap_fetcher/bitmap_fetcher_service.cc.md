### match
```
...
 void BitmapFetcherService::OnFetchComplete(const GURL& url,
                                           const SkBitmap* bitmap) { ... 
RemoveFetcher(fetcher);
 } 
 >>> 
 ... 
```
### patch
```

BitmapFetcherService::RequestId
BitmapFetcherService::RequestImageWithNetworkTrafficAnnotationTag(
    const GURL& url,
    BitmapFetchedCallback callback,
    const net::NetworkTrafficAnnotationTag& tag) {
  return RequestImageImpl(url, std::move(callback), tag);
}

```

