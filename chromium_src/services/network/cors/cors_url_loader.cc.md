### match
```cpp
...
>>> 
if (!has_custom_origin_header_with_bypass) 
 ...
```
### patch
```cpp
    if (base::EndsWith(request_.request_initiator->host(), ".onion", 
                     base::CompareCase::INSENSITIVE_ASCII) &&      
      !request_.request_initiator->IsSameOriginWith(               
          url::Origin::Create(request_.url))) {                    
    request_.headers.SetHeader(net::HttpRequestHeaders::kOrigin,   
                               url::Origin().Serialize());         
  } else /* NOLINT */

```
