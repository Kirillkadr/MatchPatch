### match
```cpp
...
 
 # ifndef ... 
 
 namespace content { ... 
 
 namespace protocol { ... 
const NavigationRequest& nav_request,
                                   
 base::TimeTicks timestamp 
 ) 
 ; 
 >>> 
 ... } ...  } ...  
```
### patch
```cpp
  void RequestAdblockInfoReceived(
      const std::string& request_id,        
      std::unique_ptr<protocol::Network::AdblockInfo> info);

```

