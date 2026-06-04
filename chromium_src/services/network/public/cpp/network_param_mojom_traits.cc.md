### match
```cpp
...
 
 namespace mojo { ... 
 
 bool StructTraits<network::mojom::HostPortPairDataView, net::HostPortPair>::
    Read(network::mojom::HostPortPairDataView data, net::HostPortPair* out) { ... 
if (!data.ReadHost(&host)) {
    return false;
  }
 *out = net::HostPortPair(std::move(host), data.port()); 
 >>> 
return true;
 ... } ...  } ...  
```
### patch
```cpp
  std::string username;
  if (!data.ReadUsername(&username)) {
    return false;
  }
  out->set_username(username);

  std::string password;
  if (!data.ReadPassword(&password)) {
    return false;
  }                                             
  out->set_password(password);

```

