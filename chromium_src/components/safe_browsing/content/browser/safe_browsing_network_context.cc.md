### match
```cpp
...
 
 class SafeBrowsingNetworkContext::SharedURLLoaderFactory
    : public network::SharedURLLoaderFactory { ... 
>>> 
 std::move(loader) 
 , 
 request_id 
 , 
 options 
 , 
 request 
 , 
 std::move(client) 
 , 
<<< 
...} ...  
```
### patch
```cpp
        std::move(loader), request_id, options, request,network::SystemRequestHandler::GetInstance()->OnBeforeSystemRequest(request)std::move(client),

```

