### match
```cpp
...
 
 # ifndef ... 
 
 static uint16_t port(const net::HostPortPair& host_port_pair) { ... 
return host_port_pair.port();
 } 
 >>> 
 ... 
```
### patch
```cpp
  static const std::string& username(            
      const net::HostPortPair& host_port_pair) { 
    return host_port_pair.username();            
  }                                              
                                                 
  static const std::string& password(            
      const net::HostPortPair& host_port_pair) { 
    return host_port_pair.password();            
  }

```

