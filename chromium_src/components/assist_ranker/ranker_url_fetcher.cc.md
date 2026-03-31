### match
```cpp
...
 
 namespace assist_ranker { ...   >>> 
 bool 
 RankerURLFetcher::Request 
 (  <<< 
const GURL& url
 ... ) ...  } ...  
```
### patch
```cpp
bool RankerURLFetcher::Request_ChromiumImpl(

```

### match
```cpp
...
 
 namespace assist_ranker { ... 
 
 void RankerURLFetcher::OnSimpleLoaderComplete(
    std::optional<std::string> response_body) { ... 
std::move(callback_).Run(state_ == COMPLETED, data);
 } 
 >>> 
 ... } ...  
```
### patch
```cpp
bool RankerURLFetcher::Request(
    const GURL& url,
    RankerURLFetcher::Callback callback,
    network::mojom::URLLoaderFactory* url_loader_factory) {
  return false;
}

```

